react-useContext

Ein useContext Konstrukt umfasst drei Teile

1. Definition des Kontextes: createContext

2. Füllen des Kontextes, üblicherweise in einer Komponente. context Provider

2.1 Inneren Kontext und äusseren Kontext gebrauchen.
<div>
  <ColorContext.Provider value="orange">
    <h3>Color choice</h3>
  </ColorContext.Provider>
</div>


3. Nutzen des Kontextes, üblicherweise in einer Komponente. useContext

const color = useContext(ColorContext);
//    ^^^^^              ^^^^^^^^^^^^
//    context value      context

Im Beispiel wird an zwei Stellen eine Farbe eingestellt werden.
Diese Farbe wird an weiteren zwei Stellen ausgelesen.

Mögliche Alternativen:
A) useState und dann den Zustand den DOM-tree herumreichen.
B) Vollständige State-Mechanismen, wie MobX

Referenzen
A) React-Dokumentation: https://react.dev/reference/react/useContext