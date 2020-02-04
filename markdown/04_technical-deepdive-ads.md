<!-- .slide: data-background="assets/neon-lights.jpg" -->

# Werbung

---

## Werbung = 💰💰💰

✅ Werbung finanziert Journalismus<br><span class="fragment">(zumindest noch)</span>

---

## Aber… 😭

* Werbung ist eher nicht responsive
* Hunderte Requests und Scripte verlangsamen die Seite
* Der Lesefluss leidet unter auf- und zuklappenden Werbeslots
* Sticky Werbung legt sich gerne mal über Navigationselemente
* Und manche Werbung ist gekommen, um Deine Daten zu stehlen

---

## Standardformate

Online-Werbung wird in Anlehnung an Zeitungswerbung immer noch in festen Formaten verkauft.

---

<!-- .slide: data-background="assets/banner-sizes.jpg" -->

---

## Kein responsiver Code

Es gibt traditionell zwei separate Code-Snippets, einmal für Desktop, einmal für Mobile.

Tablets fallen als Gerätekategorie komplett unter den Tisch. <!-- .element: class="fragment" -->

---

## Lösung?

```html
<div class="ad">
  <script>
    var mobileMQ = matchMedia('(max-device-width: 20em)');
    
    if (mobileMQ.matches) {
      // Mobile Code
    } else {
      // Desktop Code
    } 
  </script>
</div>
```

---

## Nein

Denn Werbesnippets bestehen aus einer  
Mischung aus HTML und Inline-Script:

```html
<div id="mobilebanner"></div>
<script>
  displaySlot("mobilebanner");
</script>
```

(vereinfacht)

---

```html
<div class="ad">
  <noscript class="mobile">
    // Mobile HTML Code
  </noscript>
  <noscript class="desktop">
    // Desktop HTML Code
  </noscript>
</div>
<script>
  // 1. Code per .textContent aus dem passenden 
  // <noscript> ziehen
  // 2. Code per .innerHTML ins <div class="ad">
  // stecken 
</script>
```

---

## Nein

Denn per `.innerHTML()` eingefügte `<script>` Elemente werden nicht ausgeführt.

```html
<div id="mobilebanner"></div>
<script>
  displaySlot("mobilebanner");
</script>
```

---

## Jetzt aber… Lösung!

```html
<div class="ad">
  <template class="mobile"><!-- HTML --></template>
  <template class="desktop"><!-- HTML --></template>
  <script>
  var mq = matchMedia('(max-device-width:20em)');
  var ad = document.currentScript.closest('.ad');
  var content = ad.querySelector(
      mq.matches ? '.mobile' : '.desktop'
      ).content;

  ad.appendChild(document.importNode(content, true));
  </script>
</div>
```

---

<!-- .slide: data-background="./assets/zombie-graveyard.jpg" -->

![Internet Explorer Logo](assets/browser-logos/internet-explorer_9-11/internet-explorer_9-11_512x512.png) <!-- .element: class="transparent" -->

---

<!-- .slide: data-transition="fade" data-background="./assets/windows-7-wallpaper.jpg" -->

Internet Explorer kennt weder `<template>`,  
noch `document.currentScript`.

---

![Screenshot des Blogposts "Dealing with Ads in 2020"](assets/blogpost-dealing-with-ads.png) <!-- .element: class="autoheight" style="width: 360px" -->

[schepp.dev/posts/ad-integration-in-2020/](https://schepp.dev/posts/ad-integration-in-2020/)

---

## Was ist mit den 7% Tablets?


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

```html
<meta name="viewport" content="width=device-width">

<script>
  if (matchMedia('(min-width: 45.3125em)').matches) {
    document
      .querySelector('[name="viewport"]')
      .setAttribute('content', 'width=1325');
  }
</script>
```

---

![RP ONLINE auf einem Tablet](assets/rp-online-ipad.png) <!-- .element: class="transparent" style="width: 500px; min-width: 0" -->

---

<!-- .slide: data-background="assets/bad-reception.jpg" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Keine Werbung bei langsamer Verbindung

---

```js
function hasFastConnection() {
  if (navigator.onLine === false) { return false; }
  
  if (!navigator.connection) { return true; }
  
  switch (navigator.connection.effectiveType) {
    default:
      return true;
    
    case 'slow-2g':
    case '2g':
      return false;
  }
}
```

---

![Chrome Devtools schalten Werbung ab bei niedriger Geschwindigkeit](assets/disabling-ads-for-slow-connections.png)

---

<div class="side-by-side" style="width: 80%; margin: 0 auto">

<video autoplay muted loop>
<source data-src="assets/position-sticky-ad.mp4" type="video/mp4" />
</video>

<div style="text-align: left">

## Layout-Stabilität mit Sticky Ads

Wenn entsprechend aktiviert, wird das Werbemittel mit `position: sticky` ausgerüstet.

</div>
</div>

---

## Achtung

`position: sticky` geht auf der Stelle kaputt, wenn auch nur eines der Eltern-Elemente weiter oben im DOM Baum `overflow : hidden` nutzt 🧨

---

<!-- .slide: data-background="assets/man-on-highest-block.jpg" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Den z-Index Krieg gewinnen

---

<div class="side-by-side"style="width: 100%; margin: 0 auto">

<div id="stacking" class="livecoding-result">
  <div class="navigation"></div>
  <div class="wrapper">
    <div class="ad"></div>
  </div>
</div>

<pre><code class="liveCoding css" data-livecoding-id="stacking" contenteditable>.navigation {
  position: absolute;
  z-index: 1;
}

.wrapper {
}

.wrapper .ad {
  position: absolute;
  z-index: 1000;
}</code></pre>

</div>

---

Werbung hängt sich immer an `document.body`.

```html
<div class="fakebody"></div>
```

```css
.fakebody {
  position: relative;
  z-index: 0;
}
```

```js
Object.defineProperty(document, 'body', {
  get() { return document.querySelector('.fakebody') }
});
```

---

## Sicherheit

![Facebook Pixel graift auf input.value zu](assets/facebook-accesses-input.jpg)

Facebook Pixel

---

## Inputs gegen Auslesen absichern

1\. Echten Zugang zu `.value` wegspeichern:

```js
const realValue = Object.getOwnPropertyDescriptor(
                    HTMLInputElement.prototype, 
                    'value'
                  );
```

---

2\. Neue Property namens `.realValue` für den Zugriff definieren:

```js
Object.defineProperty(
  HTMLInputElement.prototype, 
  'realValue', 
  {
    get() { return realValue.get.call(this) },
  }
);
```

---

3\. Dafür sorgen, dass bei Abfrage von `.value` immer nur ein leerer String zurück kommt: 

```js
Object.defineProperty(
  HTMLInputElement.prototype, 
  'value', 
  {
    get() {
      console.trace('A script just tried to access\
                   an input\'s value', this);
      return '';
    },
  }
);
```

---

<!-- .slide: data-background="assets/phew.gif" -->

