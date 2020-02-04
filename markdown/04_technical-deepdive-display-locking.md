<!-- .slide: data-background="assets/painted-canvas.jpg" -->

# Display Locking

---

Also, die Startseite, die ist ja lang…

<video autoplay muted>
<source data-src="assets/scrolling-homepage-desktop.mp4" type="video/mp4" />
</video>

---

## Ergebnis: Lange Renderzeiten

<!-- .slide: data-transition="fade" -->

![Chrome Profilder zeigt knapp 14 Sekunden reine Renderzeit](assets/display-locking-off.png)

<p>&nbsp</p>
---

## Ergebnis: Lange Renderzeiten

<!-- .slide: data-transition="fade" -->

![Chrome Profiler zeigt knapp 14 Sekunden reine Renderzeit, hervorgehoben](assets/display-locking-off-highlighted.png)

<p class="blink fragment">14 SEKUNDEN!!! 😭</p>

---

## Muss die Seite so lang sein?

TL;DR: Ja!

* SEO möchte gerne viele Links haben
* Jedes Ressort möchte vertreten sein
* Redakteure haben die Menge nicht im Blick

---

## Die Lösung?

---

## Display Locking!

> Render Subtree (a.k.a. Display Locking) is designed to allow developers and browsers to easily scale to large amount of content and control when rendering work happens.

---

`rendersubtree="invisible"`

```html
...
<section rendersubtree="invisible"></section>
<section rendersubtree="invisible"></section>
<section rendersubtree="invisible"></section>
...
```
---

<div class="perspective">
<span class="fragment"></span>
<img src="assets/homepage-display-lock.png" alt="Startseite mit aktivem Display Lock" class="zoom">
</div>

---

Lokal testbar via Browser-Flag

`chrome://flags/`

![Display Locking in den Chrome Flags](assets/chrome-flags-display-locking.png)

---

Für alle Besucher der Seite aktivierbar per "Origin Trial"

![Googles Origin Trials Seite](assets/origin-trials.png)

[developers.chrome.com/origintrials/](https://developers.chrome.com/origintrials/)

---

Origin Trial Token 

```html
<meta http-equiv="origin-trial" 
      content="Ah+c5l+ginn32...jp0cnVlfQ==">
```

---

## Vorher/Nachher-Vergleich

<!-- .slide: data-transition="fade" -->

vorher:  
![Chrome Profiler zeigt knapp 14 Sekunden reine Renderzeit, hervorgehoben](assets/display-locking-off-highlighted.png)

---

## Vorher/Nachher-Vergleich

<!-- .slide: data-transition="fade" -->

nachher:  
![Chrome Profiler zeigt knapp 7 Sekunden reine Renderzeit, hervorgehoben](assets/display-locking-on-highlighted.png)

---

<!-- .slide: data-background="assets/success.gif" -->

---

Hinweis: Ab Chrome 82 dann via CSS anstatt HTML:

```css
section {
    render-subtree: invisible;
}
```

