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
          .forEach((elem) => { 
            //  Element initialisieren
          });
        });
```

---

## Nachteile

Bis `DOMContentLoaded` ausgelöst wird, also alles HTML empfangen ist, vergehen auf unserer Startseite fast 5 Sekunden!

![Webpagetest Testbericht mit DOMContentLoaded bei 4,7 Sekunden](assets/domcontentloaded.png)

---

## Nachteile

Es werden ausnahmslos alle Elemente erfasst und initialisiert, egal ob sie gerade sichtbar sind, oder nicht.

![Webpagetest Testbericht mit DOMContentLoaded bei 4,7 Sekunden](assets/domcontentloaded.png)

---

```
const mObserver = new MutationObserver((mutations) => {
  mutations.forEach((mutation) => {
    // mutation.addedNodes <- look!
    // mutation.removedNodes
    // mutation.attributeName
    // mutation.oldValue
  });
});

mObserver.observe(document.documentElement, {
  attributes: false,
  childList: true,
  characterData: false,
  subtree: true,
});
```

