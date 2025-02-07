## Quellen

* dotnetpro, 1.2022, Jan Fellien, Seite 70ff

## Einführung

"CQRS ist eine Idee mit sehr vielen Ausprägungen."
CQRS treibt die Trennung von lesen und schreiben einer Software auf Systemebene.
Folgende Ideen werden erweitert

- Von Alan Kay, dass Objekte über Nachrichten kommunizieren und nicht über Methodenaufrufe.
- Von Bertrand Meyer, die Trennung von Methoden, welche lesen ohne Seiteneffekte und Methoden,
  welche den Zustand eines Objektes ändern.

## Bestandteile

### Events und Event sourcing

Die Events werden aufgezeichnet und fachlich begründet. Anstatt dass die Adresse geändert wird,
heisst der Event "PersonHasMoved" und die neue Adresse ist im Event enthalten.
Die Events werden zeilich geordnet aufgezeichnet.

Event Sourcing erlaubt das Herleiten der Daten und der Gründe weshalb sie so sind. Wann hat sich die Adresse geädert?
Wann das Datum des letzten Gesundheitschecks. Es wird nicht die Entität geändert, sondern der Stream der Events 
(Umzug, Gesundheitscheck). 

### Implementationen

#### Apply Lifecycle

Für einen neuen Event wird das Aggregat, eine fachliche Transaktionsgrenze, geladen. Zum Aggregat werden
alle Events geladen und nacheinander ausgeführt. Das Aggregat bekommt damit den aktuellen Zustand.
Aus einem Command "MovePerson" wird ein Event "PersonHasMoved" erzeugt. Die Methode "OnPersonHasMoved(PersonHasMoved event)" 
wird im Beispiel über Reflektion gefunden. Am Schluss wird das Readmodell aktualisiert.
Event sourcing kann auch ohne CQRS verwendet werden.

#### Event Stream auswerten

Bei diesem Modell wird nicht jedesmal eine Entität hergestellt. Es wird ausschliesslich nach Events im Stream gesucht, welche
die aktuell benötigten Daten herleitet. Die Frage "Wann war der letzte Arzttermin?" kann aus den Events "ArztVisited"
herausgelesen werden. Beispiel aus dem Artikel: Um herauszufinden ob eine Person heiraten darf, müssen die zeitliche Abfolge
von früheren Heiraten und Scheidungen untersucht werden.

#### In der Cloud

Es wird weiterhin vor allem der Eventstream ausgewertet. Vereinfachend werden die Events gefilert ausgelesen. Anfragen
werden von einem UI an spezielle Endpunkte gesendet. Diese können als serverless Funktionen implementiert sein. Durch 
weniger Infrastrukturcode, sollen die Events fachlich reicher implementiert werden können.
Die Commandhandler entfallen, an Stelle treten die Endpunkte, welche eine fachliche Anfrage beantworten können.
Beispiel: https://github.com/jfellien/azure-serverless-cqrs
TODO broadcasting lesen

