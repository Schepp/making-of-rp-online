<!-- .slide: data-background="assets/transformer.jpg" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

# Initialisierung

---

## Der Klassiker

```js
document.addEventListener('DOMContentLoaded', () => {
  document.querySelectorAll('.element')
          .forEach(elem => { 
            // Element initialisieren
          });
        });
```

---

## Nachteil

Nachträglich eingefügte Komponenten müssen per Hand "nach-initialisiert" werden.

---

## Noch ein Nachteil

Bis `DOMContentLoaded` ausgelöst wird, also alles HTML empfangen ist, vergehen auf unserer Startseite fast 5 Sekunden!

![Webpagetest Testbericht mit DOMContentLoaded bei 4,7 Sekunden](assets/domcontentloaded.png)

---

## Hallo Mutation Observer!

```js
const observer = new MutationObserver(mutations => {
  mutations.forEach(mutation => {
    // mutation.addedNodes <- da!
  });
});

observer.observe(document.documentElement, {
  childList: true,
  subtree: true,
});
```

---

```js
mutation.addedNodes.forEach(node => {
  if (node.nodeType !== 1) return;
  
  if (node.matches('.element')) {
    // Element initialisieren
  } 
});
```

---

```js
const initMap = {
  '.element'(node) { /* Initialisierungsfunktion */ },
};

mutation.addedNodes.forEach(node => {
  if (node.nodeType !== 1) return;
  
  Object.keys(initMap).forEach(selector => {
    if (node.matches(selector)) {
      initMap[selector](node); // Funktion ausführen
    }     
  });
});
```

---

## Mutation Observer Fallstricke

Der Mutation Observer registriert nur die äußerste eingefügte Node, wenn man `innerHTML` benutzt. 

Lösung: zusätzliches inneres `querySelectorAll()` & Buch führen!

---

```js
const processedNodes = new WeakSet();

mutation.addedNodes.forEach(node => {
  if (node.nodeType !== 1) return;
  
  [node, ...node.querySelectorAll('*')].forEach(n => {
    if (processedNodes.has(n)) return;
    
    // Abklappern der registrierten Selektoren…

    // Zum Schluss die Node als "gesehen" festhalten 
    processedNodes.add(n);
  });
});

``` 

---

## Mutation Observer Fallstricke

Internet Explorer ist mit ES5 Array-Built-ins wie `.forEach()` überraschend langsam. 

Lösung: klassische `for`-Loops!

---

## Going Beyond

Sowohl beim Mutation Observer, als auch bei `DOMContentLoaded` werden ausnahmslos alle Elemente erfasst und initialisiert.

<div class="measure">
    <div class="measure__visible">4%</div>
    <div class="measure__invisible">96%</div>
</div><img src="assets/full-rp-online-homepage-highlighted.jpg" alt="Gesamte RP-ONLINE Startseite" class="fullpage fullpage-zoom">

---

## Hallo Intersection Observer!

![Intersection Observer Demo](assets/intersection-observer.gif) <!-- .element: style="width: auto; min-width: 0; margin-top: -1em" -->

[developers.google.com/web/updates/2016/04/intersectionobserver](https://developers.google.com/web/updates/2016/04/intersectionobserver)

---

```js
const observer = new IntersectionObserver(entries => {
  // Löst bei Sichtbarkeitsänderung aus
  
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      // Das Element entry.target ist im Viewport
    }
  });
}, {
  rootMargin: '100px 50px 300px 50px', // Pufferzone
  threshold: 0.001,
});

observer.observe(node);
```

---

## In Utility-Methode gekapselt

Bei uns steckt all das, und noch mehr, gekapselt im `window.park.observer`.

```js
window.park.observer.initialize('.element', elem => {
  // elem wird hier initialisiert
}, [lazy=true/false]);
```

Standardmäßig wird "lazy" initialisiert, per optional gesetztem Parameter lassen sich Elemente auch sofort initialisieren.  