<!-- .slide: data-background="assets/widgets.jpg" -->

# Widgets&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

## Widgets auf RP ONLINE

![Wettermodul](assets/weather-widget.png)
---

## Widgets auf RP ONLINE

![Login](assets/login-widget.png) <!-- .element: class="autoheight" style="width: 300px" -->

---

![Twig.js Logo](assets/twig.js.png) <!-- .element: class="autoheight" style="width: 300px" -->

[github.com/twigjs/twig.js](https://github.com/twigjs/twig.js/)

---

## +

---

## Web Worker

---

## +

---

&nbsp;

## morphdom

[github.com/patrick-steele-idem/morphdom](https://github.com/patrick-steele-idem/morphdom)

---

## +

---

&nbsp;

![Redux Logo](assets/redux.png) <!-- .element: class="transparent" style="min-width: 0; width: 400px" -->

[redux.js.org](https://redux.js.org/)

---

## =

---

&nbsp; <!-- .element: class="fragment" -->

<h2 style="line-height: 1.5">R<span class="text-reveal">eactive&nbsp;</span>P<span class="text-reveal">rogramming</span> ONLINE</h2>

&nbsp;
---

```js
window.park.app({
  container: 'sample', // where to render into
  component: 'sample', // template to use
  reducer,
}).then((app) => {
  app.bindEvent('keyup', 'input', (e) => {
    app.store.dispatch({
      type: 'UPDATE',
      value: e.target.value,
    });
  });
});
```

Widget-Logik / Controller

---

```js
const reducer = (state, action) => {
  switch (action.type) {
    case 'UPDATE':
      state.name = action.value;
      break;

    default:
      break;
  }
  return state;
}
```

Store

---

```twig
<div class="sample">
  <h1>Hello {{ name }}!</h1>
  
  <label>
    Enter your name:
    <input name="name">
  </label>
</div>
```

Template / View

---

## Multithreading

Twig.js wird in einem Web Worker ausgeführt:

![Chrome Profiler zeigt aktive Web Worker](assets/profiler-webworker.png)

---

## Server Side Rendering?

Wird ein Widget Slot mit einen initialen State konfiguriert, wird das Widget schon serverseitig gerendert und dann clientseitig hydriert (ohne Re-Rendering).

```json
{
  "type": "search", // Controller
  "component": "search", // View
  "initialState": { … }
}
```

---

## Woher holt sich der Renderer die Templates?

Per AJAX aus einer `widgets/templates.json`, die alle Komponenten-Templates in einer Map enthält:

```json
{
  "button.twig": "<button>{{ label }}</button>",
  "login.twig": …,
  …
}
```

---

## Stats

| Bestandteil             | Größe       |
|-------------------------|-------------|
| Core + morphdom + Redux | 23 KB       |
| twig.js + Web Worker    | 87 KB       |
| Templates               | 335 KB      |
| Templates (GZIP'ed)     | 60 KB       |
