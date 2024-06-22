<!--
.. title: React
.. date: 2024-06-22
.. tags: React
.. type: text
.. has_math: false
-->

## Quellen

- Buch "The Road to React", Robin Wieruch, 2023
- Buch "", Kapitel, 2022
- Diverse online Quellen, verlinkt


## Aufsetzen

```bash
npm create vite@latest
```

Es folgt ein Assistent um ein React Projekt aufsetzen zu können.

## Begriffe

```typescript
// Das ist ein Hook, darf nur in einer Methode aufgerufen werden.
const [count, setCount] = useState(0);
```

Funktionen, welche mit **use** beginnen, werden Hooks genannt. Sie
dürfe nicht in Schlaufen oder Bedingungen stehen. Sonst muss eine
weitere Komponente extrahiert werden.

**useState** und **useEffect** sind die häufigsten Hooks in React.

useEffect: um Seiteneffekte mitzubekommen.
useContext: Advanced feature

## Buchnotizen

// Umbruch in reader, zb. S33/179 oben .eslintrc
// Vielleicht ein Schema wie eslint, plugin und config zusammen hängen. commit b862f6b

### Bootstrapping

Mit ReactDOM wird ein Teil eines html Files ersetzt.
Typischerweise heisst die Startkomponente ``App``.

Die beiden Sachen heissen
function declaration oder arrow function

Es gibt syntetische Events wie z.B. onChange von React selbst, aufrufen mit
onChange="{myHandleFunction}", Achtung ohne Klammern in ...Function().

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

## Unterschiede Angular

* keine Kommandozeile
  * z.B zum Anlegen einer Komponente, einer Pipe oder eines Services.
  
* bei Angular müssen Abhängigkeiten einerseits mit ng update und andererseits
  mit dem gewöhnlichen Paketmanager (npm, yarn, ...) verwaltet werden, im
  selben package.json File.
  
* Starten einer neuen Anwendung aufwändiger, siehe....
