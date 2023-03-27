# Awaiting async Tasks

## Sources

- Zeitschrift dotnetpro.de 2/2018, Seiten 23ff, Daniel Marbach
- https://devblogs.microsoft.com/dotnet/configureawait-faq/, abgerufen 25. März 2023, Stephen Toub

## Tasks

Es gibt _IO bound_ Tasks und _CPU bound_ Tasks.

Immer geschieht die Arbeit auf Threads, bei IO Task aus dem IO-Threadpool, bei CPU bound Tasks aus dem
Worker-Threadpool.

Bei _CPU bound Tasks_ ist die Beziehung zum Thread 1:1, bei IO kann ein Thread mehrere IO bound Tasks nebenläufig abarbeiten. IO bound Tasks werden vom IO-Completion-Port notifiziert, wenn die Operation beendet worden ist.

Es kann nicht immer entschieden werden, um welchen Typ von Task es sich handelt.

## Definitionen

- _Nebenläufigkeit_
  - Während dem die Waschmaschine läuft, räume ich den Geschirrspüler aus. 

- _Parallelität_ 
  - Unsere 200 Weingläser werden von vier Personen gleichzeitig abgetrocknet. 

- _System.Threading.SynchronizationContext_
  - Hat eine virtuelle Methode `Push`. Überschreibungen für WPF, Winforms, ASP.Net etc.
  Normalerweise Weiterleitung nach `ThreadPool.QueueUserWorkItem` mit Argumenten (Delegate, Objektzustand). Gibt es schon lange in der .Net Welt. Ist nicht an einen Thread gebunden.
  Ist eine allgemeine Abstraktion eines Schedulers. Gehört zu einem AppModel. Kann `null` sein.

- _System.Threading.Tasks.TaskScheduler_
  - Eine Abstraktion eines Schedulers für Tasks. Task erhält seinen Scheduler beim Start. Standardimplementation geht auf `ThreadPool`.
  Kann mit `FromCurrentSynchronizationContext ` erstellt werden.
  Führt mit `TryExecuteTask(Task)` einen Task aus.

- _Capturing_
  - async / await berücksichtigt SynchronizationContext und TaskScheduler, kostet Laufzeit.

### Zusammenhänge

`ConfigureAwait(false)` ignoriert das _Capturing_ siehe oben. - Callbacks sind nicht gezwungen, auf dem gekaperten Context ausgeführt zu werden; das spart Zeit.
- Deadlocks: Gegeben der Context erlaubt bloss eine Operation, wenn eine Netzwerkoperation fertig ist, kann sie nicht auf den Context zugreiffen, da der einzige Zugriff bereits vom startenden Thread beansprucht wird.

ConfigureAwait(true) wird nicht gebraucht, damit findet das _Capturing_ statt.

`ConfigureAwait(false)` überschreibt den Context, kann gefährlich sein für App-Code!

Mit async / await wird Ablaufreihenfolge garantiert, mit ConfigureAwait(false) kann der Context übersteuert werden.

ConfigureAwait(false) allgemein für Libraries, Ausnahme wenn Library Code für App ausführt, z.B. in einem Callback.

`Task.Run` hat keinen Context, ConfigureAwait(false) hat also keinen Effekt.

## Stolpersteine

Starten eines Tasks mit `Task.Run()`, weil immer der **Default-Scheduler** des Threadpools genommen wird.
`Task.Factory.StartNew()` nimmt den **CurrentScheduler**, kann z.B. bei UI-Anwendungen der Dispatcher Thread sein.
