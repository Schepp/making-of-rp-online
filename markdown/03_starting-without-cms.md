# Frontend-Architektur
---
## Übergeordnete Ziele

<ul>
    <li class="fragment">Gut skalierbar</li>
    <li class="fragment">Nachvollziehbar und wartbar</li>
    <li class="fragment">Performant</li>
    <li class="fragment">Sicher</li>
    <li class="fragment">Barrierefrei</li>
    <li class="fragment"><blink>_</blink></li>
</ul>
---
## Zielgruppe

<canvas data-chart="bar">
<!-- 
{
 "data": {
  "labels": [
    "Smartphones",
    "Tablets",
    "Desktops"
  ],
  "datasets": [
   {
    "data": [
        67.15,
        25.69,
        7.17
    ],
    "label": "Gerätklasse","backgroundColor":"rgba(21,174,25,1)"
   }
  ]
 }, 
 "options": { "responsive": "true" }
}
-->
</canvas>

---
## Zielgruppe

<canvas data-chart="bar">
<!-- 
{
 "data": {
  "labels": [
    "Chromium",
    "Safari",
    "Firefox",
    "Edge",
    "Internet Explorer"
  ],
  "datasets": [
   {
    "data": [
        57.36,
        27.96,
        8.21,
        3.22,
        2.99
    ],
    "label": "Browser Engines","backgroundColor":"rgba(21,174,25,1)"
   }
  ]
 }, 
 "options": { "responsive": "true" }
}
-->
</canvas>

---
<!-- .slide: data-background="./assets/windows-7.png" -->
---
## Technische Eckpfeiler

<ul>
    <li class="fragment">Moderner Stack</li>
    <li class="fragment">Komponenten-basiert</li>
    <li class="fragment">Mobile First</li>
    <li class="fragment">So wenig JavaScript wie möglich</li>
    <li class="fragment">So wenig externe Libraries wie möglich</li>
    <li class="fragment">Graceful Degradation: Alte Browser bekommen weniger</li>
    <li class="fragment">Resilienz: Voll funktional, auch bei kaputtem/abgeschaltetem JS</li>
</ul>
---
## Moderner Stack

<ul>
    <li class="fragment">HTML 5.2 und WAI-ARIA 1.1</li>
    <li class="fragment">CSS für moderne Browser (z.B. Flexbox, Grid)</li>
    <li class="fragment">SCSS als Precompiler + Autoprefixer als Post-Compiler</li>
    <li class="fragment">JavaScript nach ES6 (transpiliert nach ES5)</li>
    <li class="fragment">Gulp als Task-Runner, Webpack als Module-Bundler, Node-Tooling</li>
    <li class="fragment">Code-Style-Konventionen für die Lesbarkeit</li>
    <li class="fragment">Code-Linter zur Verhinderung von Programmierfehlern</li>
    <li class="fragment"><blink>_</blink></li>
</ul>
---
## Komponenten-basiertes Design

<ul>
    <li class="fragment">Baukastensystem: Schnelle Komposition neuer Seiten</li>
    <li class="fragment">Eine Komponente pro Usecase: DRY-Prinzip</li>
    <li class="fragment">Jede Komponente funktioniert in Isolation und ist einzeln testbar</li>
    <li class="fragment">Alle Dateien an einem Ordner: Template, CSS, JS, Doku u. Testdaten</li>
    <li class="fragment"><strike>Kein Atomic Design!</strike></li>
    <li class="fragment"><blink>_</blink></li>
</ul>
---
<div class="resizable"><iframe data-src="assets/components/opener.html" scroll></iframe></div>

[Opener-Komponente](./assets/components/opener.html)
---
<div class="resizable"><iframe data-src="assets/components/profile.html" scroll></iframe></div>

[Profile-Komponente](./assets/components/profile.html)
---

![Alles in einem Ordner](./assets/all-in-one-folder.png)

---
## HTML 5.2

```
<header>
<footer>
<aside>
<details>
<dialog>
<main>
<input type="search">
```
---
## WAI-ARIA 1.1 (Accessible Rich Internet Applications)

```
role="main"
role="search"
role="heading"
role="presentation"
role="alert"
role="tabpanel"
role="group"
role="radiogroup"
role="listbox"
role="listitem"
aria-labelledby="..."
aria-level="3"
...
```
---
## Modernes CSS

```
1rem
1vw
1vh
display: flex;
display: grid;
position: sticky;
column-width: 20rem;
filter: drop-shadow();
object-fit: cover;
pointer-events: none;
calc()
@supports() {}
...
```
---
## Mobile First CSS

```
.element {
  width: 100%;
}

@media screen and (min-width: 40em) {
  .element {
    width: 40rem;
  }
}
```
---
## CSS mit BEM: Block Element Modifier

* Klares Name-Spacing pro Komponente (Block)
* Klar Erkennbare Zugehörigkeit von DOM-Elementen (Elements) zu Komponenten
* Verhindert ungewolltes Style-Bleeding in andere Komponenten
* Ermöglicht einen problemlosen Wechsel der HTML-Semantik
* Flache CSS-Spezifität
* Sorgt für klare Zuständigkeiten (Komponente A funktioniert ohne Style von Komponente B)
* Guter IDE-Support
* Nachteil: Viel Text, wird aber durch eine gute IDE und GZIP-Kompression aufgehoben
---
<!-- .slide: data-background="images/bem.png" data-state="inverted" -->
---
## CSS mit BEM: Block Element Modifier

* Block: [blockname]
* Element im Block: [blockname]__[elementname]
* Block-Variation (Modifier): [blockname]__[variationsname]
---
## CSS mit BEM: Beispiel

```
<article class="park-breaking">
  <a href="..." class="park-breaking__link">
    +++ Eilmeldung +++
    <h2 class="park-breaking__headlines">
    <span class="park-breaking__headline">Air Berlin besitzt keine eigenen Flugzeuge mehr</span>
         : <span class="park-breaking__kicker">Nur noch geleaste Maschinen</span>
      </h2>
  </a>
</article>
```
---
## Barrierefreiheit

<ul>
    <li>Tastaturnavigierbarkeit</li>
    <li>Focus-Styles</li>
    <li>Alternativtexte für (non-dekorative) Grafiken</li>
    <li>Passende HTML-Semantik, z.B. `<a>` vs. `<button>`, Überschriftenlevels</li>
    <li>WAI-ARIA</li>
    <li>Sinnvolle Informationsstruktur bei defektem oder deaktiviertem CSS</li>
    <li>Funktionale Website auch bei defektem oder deaktiviertem JavaScript</li>
    <li>Flexibles Layout dank `rem`- und `em`-Units</li>
    <li><blink>_</blink></li>
</ul>
---
## Modernes JavaScript

Wir verwenden ES6 Syntax, weil es kompakter zu schreiben ist und wir es in Zukunft direkt an die Browser ausliefern können (auch heute ist das schon mit einem speziellen Verfahren möglich). Für alte Browser transpilieren wir nach ES5 (mit Babel).

Und wir nutzen moderne APIs:

* element.closest()
* element.matches()
* Promises
* async/await
* Fetch API
* Mutation Observer
* Intersection Observer
* Web Worker
* Service Worker
* ...

ggf. inklusive Polyfills für alte Browser
---
## Code-Styles & Linter

* editorConfig für die generelle Formatierung mit Spaces und Tabs
* ESLint für JavaScript mit der AirBnB-Vorlage, mit leichten Anpassungen
* StyleLint zum Prüfen zu tiefer Verschachtelung
* JSONLint zur Prüfung unserer Dummy-Daten
---
## Automation

Gulp als Task-Runner: 

* Transpilieren, Concaternieren, Komprimieren von JavaScript und CSS
* Vendorprefixing für CSS
* Down-Stripping des head.css
* Erzeugen von WOFF- und WOFF2-Schriftformaten aus TTF
* SVG Optimieren und SVG-Sprites Erzeugen
* Aufbereitung der Templates für unseren clientseitigen Renderer
* Rendern von Dummy-Seiten, EinzelKomponenten und Komponenten-Browser
