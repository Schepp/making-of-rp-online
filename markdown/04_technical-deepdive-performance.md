<!-- .slide: data-background="assets/speed.jpg" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

# Performance

---

## Preloaden der Fonts

```html
<link rel="preload" 
      href="Merriweather-Regular.woff2"
      as="font"
      crossorigin="anonymous">
```

---

## Preconnecten & Preloaden von Werbeplattformen

```html
<link rel="preload" 
      href="//www.googletagservices.com/tag/js/gpt.js"
      as="script">
```

```html
<link rel="preconnect" 
      href="//securepubads.g.doubleclick.net">
<link rel="dns-prefetch" 
      href="//securepubads.g.doubleclick.net">
```
---

## JavaScript

ES6 für moderne Browser, transpiliertes ES5 für alte Browser:

<div class="side-by-side">

```html
<script type="module" 
        crossorigin 
        async
        src="main.es6.js"></script>
<script nomodule 
        async
        src="main.js"></script>
```

| Variante               | Größe       |
|------------------------|-------------|
| main.es6.js            | 86 KB       |
| main.js                | 110 KB      |
| main.js + Polyfills    | 238 KB      |

</div>

---

## Polyfills nur bei Bedarf

```html
<script>
if (!window.Promise) {
  document.write(
  '<script src="babel-polyfill.js"></'
  + 'script>');
}
if (!window.IntersectionObserver) {
  document.write(
  '<script src="intersection-observer-polyfill.js"></'
  + 'script>');
}
</script>
```

---

## "Above the Fold" Ressourcen

```html
<link rel="preload" href="head.css" as="style">
<script>
  var styles = localStorage.getItem('head.css');

  if (styles) {
    document.write('<style>' + styles  + '</style>');
  } else {
    document.write(
      '<link href="head.css" rel="stylesheet">');
  }
</script>
```

---

## Ähm… Service Worker?

Der Service Worker ist aufgrund asychronen APIs zu "langsam"! 

```js
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.open('cache').then(cache => 
      cache.match(event.request).then(response => 
        response
      )
    )
  );
});
```

---

## Lazy-ladende Bilder

```html
<div class="image">
<svg width="950" height="526" class="image__sizer"/>
  <noscript>
    <img src="data:image/svg+xml,%3Csvg xmlns='…' 
              width='950' height='526' %3E%3C/svg%3E" 
         srcset="…" sizes="…" alt="…"
         width="950" height="526"
         async="on" decoding="async"
         class="image__image">
  </noscript>
</div>
```

---

## Weniger DOM durch "lazy" HTML

<video autoplay muted>
<source data-src="assets/lazy-html.mp4" type="video/mp4" />
</video>
---

<!-- .slide: data-transition="fade" -->

## Weniger KB durch SVG Sprites

![RP ONLINE Startseite](assets/svg-sprite.jpg) <!-- .element: class="autoheight" -->
---

<!-- .slide: data-transition="fade" -->

## Weniger KB durch SVG Sprites

![RP ONLINE Startseite mir hervorgehobenen SVG Icons](assets/svg-sprite-highlighted.jpg) <!-- .element: class="autoheight" -->

---

```html
<svg class="sprite" xmlns="…">
    <symbol id="sprite-article" viewBox="…">
      <path d="…" fill-rule="evenodd"/>
    </symbol>    
    <symbol id="sprite-bookmark" viewBox="…">
      <path d="…" fill-rule="evenodd"/>
    </symbol>
    …    
</svg>
```

```html
<svg><use xlink:href="#sprite-article"></use></svg>
```

---

<!-- .slide: data-background="assets/speedcurve-lighthouse.png" -->

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Das Ergebnis ist ernüchternd

---

![Fast 1 Sekunde Time to First Byte](assets/network-time-to-first-byte.png)

1 Sekunde Time to First Byte 🙈

---

![Webpagetest Wasserfall](assets/waterfall.jpg)

HTTP/2 Priorisierung funktioniert nicht richtig 😭