---
title: Bootstrap
---

Bootstrap on suosituin valmis CSS-komponenttikirjasto responsiivisten
sivustojen rakentamiseen. Versiosta 5 lähtien se **ei enää vaadi
jQueryä** — oma JavaScript-nippu riittää interaktiivisille komponenteille
(modaalit, pudotusvalikot, jne.).

## Käyttöönotto CDN:ltä

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">

<!-- Ennen </body>-tagia, JS-komponentteja (modaalit, dropdownit...) varten -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
```
Lukitse aina tarkka versionumero tuotannossa (kuten yllä) — pelkkä
`bootstrap@5` osoittaisi automaattisesti uusimpaan 5.x-versioon, mikä voi
rikkoa sivuston yllättäen päivityksen yhteydessä.

## Ruudukko (grid)

```html
<div class="container">
  <div class="row">
    <div class="col-md-6">Puolet leveydestä keskikokoisella näytöllä+</div>
    <div class="col-md-6">Toinen puoli</div>
  </div>
</div>
```

| Luokka | Käyttö |
| --- | --- |
| `container` | Kiinteä, keskitetty leveys breakpointeittain |
| `container-fluid` | Aina 100 % leveys |
| `row` | Ruudukon rivi (sisältää sarakkeet) |
| `col` | Automaattisesti tasan jaettu sarake |
| `col-<n>` | Kiinteä leveys 1–12 (12-sarakejärjestelmä) |
| `col-{bp}-<n>` | Leveys tietystä breakpointista ylöspäin (esim. `col-md-6`) |

## Breakpointit

| Lyhenne | Vähimmäisleveys |
| --- | --- |
| `sm` | 576px |
| `md` | 768px |
| `lg` | 992px |
| `xl` | 1200px |
| `xxl` | 1400px |

## Yleisiä apuluokkia (utilities)

```html
<div class="d-flex justify-content-between align-items-center">...</div>
<div class="m-3 p-2">margin 3, padding 2 (Bootstrapin oma spacing-asteikko)</div>
<div class="d-none d-md-block">Piilossa pienellä näytöllä, näkyy md:stä ylöspäin</div>
<p class="text-center text-muted">Keskitetty, himmennetty teksti</p>
```
Spacing-luokat (`m-*`, `p-*`) käyttävät asteikkoa 0–5 (ja `auto`), eivät
suoraan pikseliarvoja — `m-3` vastaa oletusteemassa noin 1rem:iä.

## Painikkeet

```html
<button class="btn btn-primary">Ensisijainen</button>
<button class="btn btn-outline-secondary">Ääriviivallinen</button>
<button class="btn btn-danger btn-sm">Pieni, varoittava</button>
```

## Kortit (cards)

```html
<div class="card" style="width: 18rem;">
  <img src="kuva.jpg" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Otsikko</h5>
    <p class="card-text">Sisältöteksti.</p>
    <a href="#" class="card-link">Linkki</a>
  </div>
</div>
```

## Navigointipalkki (navbar)

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Sivusto</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#nav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="nav">
      <ul class="navbar-nav">
        <li class="nav-item"><a class="nav-link" href="#">Etusivu</a></li>
      </ul>
    </div>
  </div>
</nav>
```

## Modaali (ei JavaScriptiä itse kirjoitettavaksi)

```html
<button data-bs-toggle="modal" data-bs-target="#omaModaali">Avaa</button>

<div class="modal" id="omaModaali">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Otsikko</h5>
        <button class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">Sisältö</div>
    </div>
  </div>
</div>
```
`data-bs-*`-attribuutit ohjaavat Bootstrapin omaa JS-nippua — mitään
event listenereitä ei tarvitse kirjoittaa käsin perustapauksessa.

## Ilmoitukset (alerts)

```html
<div class="alert alert-success" role="alert">Onnistui!</div>
<div class="alert alert-danger alert-dismissible fade show">
  Virhe!
  <button class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

## Väriteemat / tumma tila (color modes, v5.3+)

```html
<html data-bs-theme="dark">
```
Voidaan asettaa myös yksittäiselle elementille (esim. `<div
data-bs-theme="dark">`) — vaikuttaa vain sen sisältöön. Perustuu CSS
custom propertyihin, joten yhdistyy hyvin myös
`prefers-color-scheme`-mediakyselyyn omalla Sass-asetuksella.

## Oman teeman muokkaus (Sass)

```scss
// omat-muuttujat.scss
$primary: #2a5db0;
$border-radius: 0.25rem;

@import "bootstrap/scss/bootstrap";
```
Muuttujat pitää määritellä **ennen** `@import`-riviä, jotta Bootstrapin
oma Sass-koodi käyttää niitä oletusarvojensa sijaan.
