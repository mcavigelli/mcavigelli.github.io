# React

## Quellen

- Buch "The Road to React", Robin Wieruch, 2023
- Buch "", Kapitel, 2022

## Begriffe

```typescript
// Das ist ein Hook, darf nur in einer Methode aufgerufen werden.
const [count, setCount] = useState(0);

useState und useEffect sind die häufigsten Hooks in React.
useState: wenn Wert über die Zeit ändert
useEffect: um Seiteneffekte mitzubekommen.
useContext: Advanced feature

## Komponenten

1. Klassenbasierte

2. Funktionsbasierte

// Umbruch in reader, zb. S33/179 oben .eslintrc
// Vielleicht ein Schema wie eslint, plugin und config zusammen hängen. commit b862f6b

## Aufsetzen

``` console
npm create vite@latest <projekt-name>-- --template react-ts

### Bootstrapping

Mit ReactDOM wird ein Teil eines html Files ersetzt.
Typischerweise heisst die Startkomponente ``App``.

Die beiden Sachen heissen
function declaration oder arrow function

Es gibt syntetische Events wie z.B. onChange von React selbst, aufrufen mit
onChange="{myHandleFunction}", Achtung ohne Klammern in ...Function().

## State

Wenn Zustand geändert wird, werden alle abhängigen Komponenten neu gezeichnet.
Gebraucht für Daten welche sich über die Zeit ändern.

''''
[currentState, stateUpdate] = useState('Essen');

current state
state updater function

State so weit unten wie möglich halten, kann über callback in props 
nach oben geschoben werden.

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

## Unterschiede Angular

* keine Kommandozeile
  * z.B zum Anlegen einer Komponente, einer Pipe oder eines Services.
  
* bei Angular müssen Abhängigkeiten einerseits mit ng update und andererseits
  mit dem gewöhnlichen Paketmanager (npm, yarn, ...) verwaltet werden, im
  selben package.json File.
  
* Starten einer neuen Anwendung aufwändiger, siehe....