# React

## Quellen

- Buch "The Road to React", Robin Wieruch, 2023
- Buch "", Kapitel, 2022
- Diverse online Quellen, verlinkt
- react.dev


function declaration oder arrow function expression!

## Aufsetzen

```bash
npm create vite@latest
```

Es folgt ein Assistent um ein React Projekt aufsetzen zu können.

## Begriffe

Live Vorschau während der Entwicklung:

**H**ot **M**odule **R**eplacement auf dem Entwicklungsserver, also z.B. vite.

**R**eact **F**ast **R**efresh auf der Client-Seite.

## Rendering jsx 101

```typescript
const title = 'Tag';
const myElement = <h1>Guten {title}</h1>;
// geht nach Vanilla JS
const myElement = React.createElement('h1', null, `Guten ${title}`);
// wird von React nach HTML transformiert
<h1>Guten Tag</h1>
```

### Loops

Schlaufen werden mit einem .map auf einem Array gerendert.

## Hooks


```typescript
// Das ist ein Hook, darf nur in einer Methode aufgerufen werden.
const [count, setCount] = useState(0);
```

Funktionen, welche mit **use** beginnen, werden Hooks genannt. Sie
dürfe nicht in Schlaufen oder Bedingungen stehen. Sonst muss eine
weitere Komponente extrahiert werden.

**useState** und **useEffect** sind die häufigsten Hooks in React.

### useEffect
Quelle https://react.dev/reference/react/useEffect

Wenn immer sich ein Wert ändert, soll etwas getan werden. Der Chatroom wird geändert von Travel nach Bicycles, dann
muss die bestehende Verbindung geschlossen werden und die neue geöffnet werden. Es kann eine Cleanup (close connection) zurückgegeben werden, welcher vor einem Wechsel ausgeführt wird.

```typescript
// source: https://react.dev/reference/react/useEffect#reference
function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');
  useEffect(() => {
    const connection = createConnection(serverUrl, roomId);
    connection.connect();
    return () => {
      connection.disconnect();
    };

  }, [serverUrl, roomId]);

    // ...

}
```

Ausführungshäufigkeit
* Liste vor Variablen
* `[]`: wird 1x ausgeführt, z.B. für das Laden von externen Daten
* kein Array, wird bei jedem Render aufgerufen 

### useReducer
Quelle: https://react.dev/reference/react/useReducer
```typescript
[state, dispatcher] = useReducer(reducer, initialArg)
```
- ``state``: ähnlich wie bei useState.
- ``reducer``: Methode, welche den state und einen Action Parameter erhält
- ``dispatcher``: UI ruft diese Methode auf, Action Parameter (siehe oben) muss mitgegeben werden

#### Vergleich mit useState
Quelle: https://www.robinwieruch.de/react-usereducer-vs-usestate/
`useState`: wenn es einfach ist, also primitive Werte sind
`useReducer`: wenn es komplexe Objekte sind, oder wenn vorher mehrere `useState` verwendet worden sind. Die Transitionslogik kann im Reducer gebündelt werden.


### Allgemeines zu Hooks

Vergleich von altem und neuem Wert wird mit ``Object.is`` gemacht.

## Buchnotizen

// Umbruch in reader, zb. S33/179 oben .eslintrc
// Vielleicht ein Schema wie eslint, plugin und config zusammen hängen. commit b862f6b



### Bootstrapping

Mit ReactDOM wird ein Teil eines html Files ersetzt.
Typischerweise heisst die Startkomponente ``App``.
index.html ruft src/main.tsx auf, welches ReactDOM importiert und dann App.tsx aufruft.

Es gibt syntetische Events wie z.B. onChange von React selbst, aufrufen mit
onChange="{myHandleFunction}", Achtung ohne Klammern in ...Function().

Häufig ruft *main.tsx* die Rootkomponente *App.tsx* auf.

## Komponenten

### Declaration
```typescript
function List() {
  return (<span>One</span>);
}
```

Eine Komponente wird einmal deklariert und kann mehrmals als **Element** 
instanziert werden.

### Instantierung
```typescript
 <List />
```

React übersetzt alle html Attribute zu React-Props. Das innere html wird ebenfalls zu einer Property *children*.

Komponenten werden deklariert und dann als React Elemente verwendet. Unter der Haube sind es alles createElement
Aufrufe.

Auch Mischungen mit createElement sind möglich:

```typescript
const Text = ({className: string, children: string}) => {
  return <p className={className}>{children}</p>
}

React.createElement(Text, {className: 'warning'}, 'Good night!')
```

Quelle: https://www.robinwieruch.de/react-element-component/


## State, useState Hook

Wenn Zustand geändert wird, werden alle abhängigen Komponenten neu
gezeichnet. Gebraucht, für Daten welche sich über die Zeit ändern.

```typescript
[money, setMoney] = useState('1000');
```

Die Syntax nennt sich **Array destructing**.

	State so weit unten wie möglich halten, kann über callback in props
	nach oben geschoben werden.

Für den Startwert **muss** kann eine Methode ``getTodos`` angegeben werden; beachte
den Unterschied zu einem Methodenaufruf ``getTodos()``.

### Schtolperschteine
2. Kann im **Strict-Mode** mehrmals aufgerufen werden.
3. Der aktualisierte Wert aus **set** ist erst im nächsten Rendercyclus
lesbar.
4. Bleibt der Wert identisch, bleibt ein Neuzeichnen aus.
5. Mit setNewValue sollen Objekte neu erstellt werden, Arrays ebenfalls
geklont und angepasst werden.
6. Wird einer Komponente ein **neuer** Key gesetzt, wird auch deren
Zustand zurückgesetzt.


## Side effects

## Componenten

### Component Composition


### Tsx

Muss ein Root-Element haben: Behelf: <Fragment> oder <> benutzen.

### Advanced

Spread operator kann gebraucht werden um alle Parameter zu übergeben
Props destrukten: immer, ausser wenn Objekt einfach weiter gereicht wird.

Daten sind readonly, von top to bottom

- Was ist Unterschied

Hier kann dekonstruiert werden.
const MyComp: React.FC<MyCompProps> = (props) => { return (null);}

und

const MyComp => (props: MyCompProps) => {return (null);}


## State und Props

Props werden von oben nach unten mitgegeben, State bleibt lokal erhalten.

Mit Callbacks kann der Zustand nach oben im Komponentenbaum gesegeben werden.

Zustand wird am lowest common denominator gespeichert.

Ausgabe abhängig vom Zustand und den Props.

### Seiteneffekte

Referenz: https://react.dev/reference/react/useEffect

Auch Seiteneffekte können einen Einfluss auf den Output haben. Beispiele sind
- local storage (TODO änderungen?)
- externe APIs, also speichern und lesen
- JavaScript eingebaute Funktionen wie Timer oder Intervalle

useState und useEffect sind die häufigst genutzten Hooks.

useEffect läuft nicht auf dem Server.

#### Übungen

https://react.dev/reference/react/useEffect#examples-connecting

Beispiele nachprogrammieren.

### Custom hooks

Scheint einfach ein Aufruf eines anderen Hooks zu sein:

```typescript
// https://react.dev/reference/react/useEffect#wrapping-effects-in-custom-hooks

function useChatRoom({ serverUrl, roomId }) {
  useEffect(() => {
    const options = {
      serverUrl: serverUrl,
      roomId: roomId
    };
    const connection = createConnection(options);
    connection.connect();
    return () => connection.disconnect();
  }, [roomId, serverUrl]);
}

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useChatRoom({
    roomId: roomId,
    serverUrl: serverUrl
  });
}


```

### Konditionales Rendering mit Ternary-Operator

```typescript
// https://react.dev/reference/react/useEffect#wrapping-effects-in-custom-hooks

function MyConditional(props : { roomId: string }) {
  return (
    <div>
      {props.roomId === "main"
      ? (<span>Main room</span>)
      : (<span>room {props.roomId} </span>)
      }
    </div>
  );
}

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useChatRoom({
    roomId: roomId,
    serverUrl: serverUrl
  });
}


```
### Daten laden
Variante mit `async / await` innerhalb von `useEffect` 
```typescript
useEffect(() => {
    const fetchData = async () => { // kein Return
        const response = await fetch("someUrl")
        const json = await response.json()
        dispatchStories({
            type: 'SET',
            payload: json.hits // keine Typisierung
        })
    }

    try {
        fetchData()
    } catch (error) {
        dispatchStories({
            type: 'SET\_ERROR',
            message: String(error)
        })
    }    
}, [])
```
### useCallback
Quelle: https://react.dev/reference/react/useCallback#skipping-re-rendering-of-components

Eine teure Komponente wird mit `memo` gecached. Eine Prop ist eine Funktion. Damit die Funktion über re-renders hinweg stabil bleibt, muss sie über `useCallback` stabil gehalten werden.
```typescript

// immer neu
function fetchProduct(pid: string) {
    // do sth
}

// selbe Funktion, so lange pid nicht wechselt
function stable = useCallback(fetchProduct, pid) // pid must be available

<ProductInfo fetch={fetchProduct} />

<ProductInfo stable={stable} />
```
#### Vergleiche / Abgrenzungen
`useMemo` hält das Resultat eines Calls vor.

### Maintenance
Mit `memo` kann eine Komponente stabilisiert werden, so dass sie nur neu gerendert wird, wenn ihre Argumente sich ändern. Das kann nützlich sein, wenn das Rendering ausschliesslich durch den Parent verursacht wird.
Werte können mit `useRef` ebenfalls stabil gehalten werden.

## Paradigmen

React ist deklarativ, kann aber auch imperativ verwendet werden.

