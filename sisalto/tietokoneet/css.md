---
title: CSS
---

## Valitsimet

```css
.luokka { }              /* class */
#id { }                    /* id */
div { }                     /* elementtityyppi */
div p { }                     /* jälkeläinen (millä tahansa syvyydellä) */
div > p { }                     /* suora lapsi */
div + p { }                      /* seuraava sisarus välittömästi */
div ~ p { }                       /* mikä tahansa seuraava sisarus */
a:hover { }                         /* pseudoluokka */
p::first-line { }                    /* pseudoelementti */
input:not([disabled]) { }             /* attribuutti + negaatio */
```

## Tärkeysjärjestys (specificity)

Yksinkertaistettuna: `!important` > inline-tyyli > ID > luokka/attribuutti/
pseudoluokka > elementtityyppi. Sama tärkeysaste ratkeaa
lähdejärjestyksen mukaan (myöhempi voittaa).

## Box model

```css
.laatikko {
  width: 200px;
  padding: 16px;
  border: 1px solid #ccc;
  margin: 8px;
  box-sizing: border-box;   /* padding+border sisältyvät width:iin, ei lisää siihen */
}
```

## Flexbox

```css
.rivi {
  display: flex;
  flex-direction: row;         /* tai column */
  justify-content: space-between;  /* pääakselin kohdistus */
  align-items: center;               /* poikittaisakselin kohdistus */
  gap: 16px;
  flex-wrap: wrap;
}

.rivi > .lapsi {
  flex: 1;             /* kasva/kutistu tasaisesti täyttääkseen tilan */
}
```

## Grid

```css
.ruudukko {
  display: grid;
  grid-template-columns: repeat(3, 1fr);   /* kolme yhtä leveää saraketta */
  grid-template-rows: auto 1fr auto;
  gap: 16px;
}

.solu {
  grid-column: 1 / 3;   /* ulottuu sarakkeesta 1 sarakkeeseen 3 */
}
```

## Muuttujat (custom properties)

```css
:root {
  --paavari: #2a5db0;
  --valilyonti: 8px;
}

.elementti {
  color: var(--paavari);
  padding: calc(var(--valilyonti) * 2);
}
```

## Mediakyselyt (responsiivisuus)

```css
@media (max-width: 700px) {
  .sivupalkki { display: none; }
}

@media (prefers-color-scheme: dark) {
  :root { --bg: #0b0f14; }
}
```

## Yksiköt

| Yksikkö | Kuvaus |
| --- | --- |
| `px` | Kiinteä pikselimäärä |
| `%` | Suhteessa vanhempaan elementtiin |
| `em` | Suhteessa elementin omaan fonttikokoon |
| `rem` | Suhteessa juurielementin (`html`) fonttikokoon — ennustettavampi kuin `em` |
| `vw` / `vh` | Prosentti näkymäalueen leveydestä/korkeudesta |
| `ch` | Numeromerkin "0" leveys — hyödyllinen tekstin lukuleveyden rajaamiseen |

## Transitionit ja animaatiot

```css
.nappi {
  transition: background-color 0.2s ease;
}
.nappi:hover {
  background-color: var(--paavari);
}

@keyframes pyoraytys {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
.spinner {
  animation: pyoraytys 1s linear infinite;
}
```
Kunnioita käyttäjän liikkeenvähennysasetusta:
```css
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !important; }
}
```

## Kerrosjärjestys

```css
.kelluva {
  position: absolute;   /* tai fixed/relative/sticky */
  z-index: 10;
}
```
`z-index` vaikuttaa vain elementteihin, joilla on `position`-arvo muu
kuin `static` (oletus).
