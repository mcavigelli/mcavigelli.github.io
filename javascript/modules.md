## Anforderungen

Anforderungen an lazy load Module:

1) Module müssen eindeutige Namen haben
2) Module müssen isoliert sein
3) Module müssen Abhängigkeiten formulieren können

## Standards

Es gibt Modulstandards, ua
* ES2015: `import` noch nicht von allen Browser benutztbar, kann auf globale Variablen kompiliert werden.
* commonjs, von Node verwendet `require('emailListModule')`, konnte mit Browserify auch im Browser verwendet werden. `require` ist immer synchron, `require` kann irgendwo im Code stehen und irgendwas enthalten -> Abhängigkeiten schwierig zu analysieren.

Es gibt Buildsysteme, ua
* webpack
* gulp

Module werden zur Compilierzeit kompiliert und aufgelöst; zur Laufzeit werden Module nachgeladen. Ohne Module konnten globale Zustände der globalen Variable `window` zugewiesen werden. IIFE Imediately invoked function expressions.

## import und export

`import {methode} from ./a`

Default exporte können ohne geschweifte Klammern importiert werden: Nutzen:
`default export function doCalc()`

oder

`export {default doCalc, bicycleColour}`

Default exports können verwendet um die Konvention eine Komponente
pro File leichter zu erreichen.

Gegensatz dazu ist named export.
`export function getPrime()`

auch möglich

`export {getPrime, bananaPrice}`

Reexportieren
```
`export * from ./a`
`export meow from ./c`
```

### Dynamische Importe

Aufteilen auf verschiedene Dateien: kann parallelisiert werden; kann z.B. im Netzwerk-Wasserfalldiagramm im Browser beobachtet werden.

**Moment.js** bietet für verschiedene Datumsformate kleinste Pakete an (lazy loading):


`let locale = await import('locale_us-en')`

Import über eine Promise über eine Funktion, vs. statisch wie sonst häufig zu sehen.

1. Stringliteral direkt an import übergeben.
2. siehe unten, braucht in tsconfig {"module": "esnext"}

```
 import {locale} from './locales/locale-us'
  
 async function main() {
    let userLocale = await getUserLocale()
    let path = ./locales/locale-${userLocale}
    let localeUS: typeof locale = await import (path)
 }
```

### Interop mit CommonJS

Mit tsconfig {"esModuleInterop": true} können Module von CommonJS oder AMD gewohnt importiert werden. `false` / default setzte zu viel an die Module voraus.

Nachteile: mehr Code generiert.

### Modus

1. Modulmodus: falls ein export oder import Statement vorliegt.
2. Skriptmodus: 
   1. globale Variablen stehen zur Verfügung, kann als `<script>` Tag importiert werden, ohne Modulsystem. // TODO mal ausprobieren.
   2. Typdeklarationen

### Namensräume

Werden nicht empfohlen, können doch Module zusammengefügt werden. Das widerspricht der Isolation von Modulen.

moduleResolution in tsconfig: Art wie nach Modulen gesucht wird.
* **node** Dateien ohne Präfix werden im `node_modules` gesucht.

* **classic** nicht empfohlen, es wird im Ordner hoch gesucht,
bis eine Datei gefunden werden kann.




### Quellen

1) Programmieren in TypeScript, Boris Cherny, Kapitel 10
2) https://medium.com/coding-at-dawn/5-reasons-i-always-prefer-default-exports-in-react-typescript-projects-c5bbe706db74
3) https://www.typescriptlang.org/tsconfig#esModuleInterop