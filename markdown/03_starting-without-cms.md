# Frontend-Architektur
---
<!-- .slide: data-background="assets/target-group.jpg" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Definition der Zielgruppe

---

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
    "label": "Gerätklasse",
    "data": [
        67.15,
        7.17,
        25.69
    ],
    "backgroundColor": [
      "#222",
      "#666",
      "#C6C6C6"
    ]
   }
  ]
 }, 
 "options": { 
    "responsive": true,
    "scales": {
      "yAxes": [{
        "ticks": {
          "beginAtZero": true
        }
      }]
    }
 }
}
-->
</canvas>

---

<canvas data-chart="bar">
<!-- 
{
 "data": {
  "labels": [
    "Chromium",
    "Safari",
    "Firefox",
    "Edge",
    "IE"
  ],
  "datasets": [
   {
    "label": "Browser Engines insgesamt",
    "data": [
        57.36,
        27.96,
        8.21,
        3.22,
        2.99
    ],
    "backgroundColor": [
      "#1DA462",
      "#006CFF",
      "#FF6611",
      "#3277BC",
      "#1EBBEE"
    ]
   }
  ]
 }, 
 "options": { 
    "responsive": true,
    "scales": {
      "yAxes": [{
        "ticks": {
          "beginAtZero": true
        }
      }]
    }
 }
}
-->
</canvas>

---

<canvas data-chart="bar">
<!-- 
{
 "data": {
  "labels": [
    "Chromium",
    "Safari",
    "Firefox",
    "IE"
  ],
  "datasets": [
   {
    "label": "Browser Engines mobil",
    "data": [
        71.95,
        26.43,
        1.24,
        0.28
    ],
    "backgroundColor": [
      "#1DA462",
      "#006CFF",
      "#FF6611",
      "#3277BC",
      "#1EBBEE"
    ]
   }
  ]
 }, 
 "options": { 
    "responsive": true,
    "scales": {
      "yAxes": [{
        "ticks": {
          "beginAtZero": true
        }
      }]
    }
 }
}
-->
</canvas>

---

<canvas data-chart="bar">
<!-- 
{
 "data": {
  "labels": [
    "iPhone 11",
    "Galaxy A50",
    "iPhone 11 Pro",
    "iPhone XR",
    "Galaxy A70"
  ],
  "datasets": [
   {
    "label": "Smartphone Verkaufscharts Oktober 2019",
    "data": [
        12,
        7,
        5,
        5,
        4
    ],
    "backgroundColor": [
      "#7D7D7D",
      "#A4C639",
      "#7D7D7D",
      "#7D7D7D",
      "#A4C639"
    ]
   }
  ]
 }, 
 "options": { 
    "responsive": true,
    "scales": {
      "yAxes": [{
        "ticks": {
          "beginAtZero": true
        }
      }]
    }
 }
}
-->
</canvas>

[Quelle: statista](https://www.statista.com/statistics/700712/smartphone-market-share-in-germany-by-model/)

---

## Samsung Galaxy A50 bei RP ONLINE

![Samsung Galaxy A50 Handy](assets/samsung-galaxy-a50.png) <!-- .element: class="transparent" -->

= 41.794 Besucher pro Tag 

---

## Highend vs. Midrange

![JavaScript Parsezeiten bei CNN](assets/devices-javascript-parse-times-cnn.png)

---
<!-- .slide: data-background="./assets/elephant-in-the-room.jpg" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Es steht noch ein Elefant im Raum…

---

<!-- .slide: data-background="./assets/zombie-graveyard.jpg" -->

![Internet Explorer Logo](assets/browser-logos/internet-explorer_9-11/internet-explorer_9-11_512x512.png) <!-- .element: class="transparent" -->

---

![Windows 7 auf jedem dritten Behörden-PC](assets/windows-7.png)  <!-- .element: class="newspaper" -->

---

<canvas data-chart="bar">
<!-- 
{
 "data": {
  "labels": [
    "IE 11",
    "IE < 11"
  ],
  "datasets": [
   {
    "label": "Internet Explorer Versionen",
    "data": [
        99.53,
        0.47
    ],
    "backgroundColor": [
      "#1EBBEE",
      "#1EBBEE"
    ]
   }
  ]
 }, 
 "options": { "responsive": "true" }
}
-->
</canvas>

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

## Technische Grundprinzipien

<ul>
    <li class="fragment">Moderner Stack</li>
    <li class="fragment">Komponentenbasiert</li>
    <li class="fragment">Mobile First</li>
    <li class="fragment">So wenig JavaScript wie möglich</li>
    <li class="fragment">So wenig externe Libraries wie möglich</li>
    <li class="fragment">Graceful Degradation: Alte Browser bekommen weniger</li>
    <li class="fragment">Resilienz: Voll funktional, auch bei kaputtem/abgeschaltetem JS</li>
    <li class="fragment"><blink>_</blink></li>
</ul>

---

> Das CMS bekommen wir erst im Oktober vom Zulieferer. Aber es nutzt wohl PHP und Twig. 

April 2017

---

<!-- .slide: data-background="./assets/stripes.png" -->

## Stack

---

## HTML 5.2

```html
<header>
  <nav>…</nav> <input type="search">
</header>
<main>
  <section>
    <article>…</article>
    <aside> <details>
      <summary>…</summary> …
    </details> </aside>
    <dialog></dialog>
  </section>
</main>
<footer></footer>
```

---

## WAI-ARIA 1.1

### Accessible Rich Internet Applications

`aria-hidden` anstatt `display: none`.

`aria-expanded="true/false"` + `aria-controls` als generische Aufklappsteuerung.

`<h3 aria-level="6">`, immer wenn SEO findet, da muss eine H3 hin, obwohl die Semantik eine H6 erfordert.

`<div role="group">` anstatt `<legend>`, das lauter Styling-Bugs hat.

---

```html
<ul role="tablist">  
  <li role="presentation">
    <a role="tab" href="#section1" 
       id="tab1" aria-selected="true">Erstes Tab</a>
  </li>
  …
</ul>  
<section role="tabpanel" 
         id="section1" 
         aria-labelledby="tab1">  
  …
</section> 
```
[Inclusive Components](https://inclusive-components.design/)

---

## CSS

### Barrierearm, Mobile-First & Modern

`rem` anstelle von `px` oder `em`. 

Media Queries mit `em`, und "Mobile First".

`display: flex` für überhaupt fast alles.

`display: grid` für Formulare.

`scroll-snap-type: x mandatory` und `scroll-behavior: smooth` für Galerien und Slider.

SCSS als Pre-Compiler + PostCSS als Post-Compiler

---

*Flexbox* & *Grid* sind flexibler und schlanker als float-basierte Grids.

*Scroll Snapping* & *Scroll Behavior* spart teure Bibliotheken ein:

| Bibliothek              | Größe       |
|-------------------------|-------------|
| Flexslider ohne jQuery  |  22 KB      |
| Flexslider *mit* jQuery | 107 KB      |
| Slick Slider            |  52 KB      |
| Swiper.js               | 136 KB      |

---

<!-- .slide: data-background="assets/windows-7-wallpaper.jpg" -->

Ähm, Moment mal…

<ul>
    <li class="fragment">Flexbox?</li>
    <li class="fragment">Grid?</li>
    <li class="fragment">Scroll Snapping?</li>
</ul>

Was ist denn jetzt mit IE? <!-- .element: class="fragment" -->

---

<!-- .slide: data-transition="fade" data-background="assets/alps.jpg" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Wer hat's erfunden?

---

<!-- .slide: data-transition="fade" data-background="assets/alps.jpg" -->

![Internet Explorer Logo](assets/browser-logos/internet-explorer_9-11/internet-explorer_9-11_512x512.png) <!-- .element: class="transparent" -->

---

## JavaScript

<!-- .slide: data-background="#F0DB4F" -->

Überall ES6, außer für inline-JavaScript.

<strong>Keine</strong> ES Module, sondern globales Utility-Objekt: `window.park`.

Für alte Browser nach ES5 transpiliert und differentiell ausgeliefert:

```html
<script type="module" crossorigin async
        src="/assets/main.es6.js?v=1"></script>
<script nomodule async
        src="/assets/main.js?v=1"></script>
```

`main.js` = 110 KB / `main.es6.js` = 86 KB
---

<!-- .slide: data-background="assets/fake-javascript.png" -->

## Sonstiges

<ul>
    <li class="fragment">Gulp als Task-Runner, Node-Tooling</li>
    <li class="fragment">Code-Style-Konventionen für die Lesbarkeit</li>
    <li class="fragment">Code-Linter zur Verhinderung von Programmierfehlern</li>
    <li class="fragment"><blink>_</blink></li>
</ul>

---

<!-- .slide: data-background="assets/building-blocks.jpg" -->

## Komponentensystem

---

## Baukastensystem

Eine Komponente pro Usecase / DRY-Prinzip

![Komponenten, die die "button" Komponente verwenden](assets/component-dependency.png)

---

## Alle Bestandteile in einem Ordner

<video autoplay muted>
<source data-src="assets/all-component-parts-in-one-folder.mp4" type="video/mp4" />
</video>

---

## Isolation

Jede Komponente wird in Isolation entwickelt und ist einzeln testbar

<div class="resizable"><iframe data-src="assets/components/opener.html" scroll></iframe></div>

---

## Backend-less

Das Frontend wird ausschließlich mit Mockdaten entwickelt.

<div class="side-by-side">
<div>

```json
{
  "type": "submit",
  "text": "Absenden"
}
```

`button/data/default.json`

</div>
<div>

```json
{
  "href": "#void",
  "text": "Linktext"
}
```

`button/data/link.json`

</div>
</div>

---

## Entwickeln von vorne nach hinten

Design 🡆 Frontend 🡆 Backend 

![Invision Apps Inspect Modus](assets/invision-inspect.png)

---

## Atomic Design

![Atomic Design Prinzipien](assets/atomic-design-process.png)

---

## Atomic Design.

> Lag mein Element jetzt im Atom- oder im Molekül-Ordner? 🤔

---

## Atomic Design?

> Mein Element ist gewachsen. Muss ich es jetzt in den Molekül-Ordner umziehen? 🤔

---

## Atomic Design? Nein!

Als sehr plakatives System hilfreich beim "Verkauf" von Komponenten-System an Stakeholder 🥩

---

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
…
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
  <a href="…" class="park-breaking__link">
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
* …

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
