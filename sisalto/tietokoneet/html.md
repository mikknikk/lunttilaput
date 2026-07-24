---
title: HTML
---

## Peruspohja

```html
<!DOCTYPE html>
<html lang="fi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Sivun otsikko</title>
</head>
<body>
  <h1>Sisältö</h1>
</body>
</html>
```

## Rakenteelliset elementit

| Elementti | Kuvaus |
| --- | --- |
| `<header>` | Sivun tai osion ylätunniste |
| `<nav>` | Navigaatiolinkit |
| `<main>` | Sivun pääsisältö (vain yksi per sivu) |
| `<article>` | Itsenäinen, uudelleenkäytettävä sisältökokonaisuus |
| `<section>` | Temaattinen osio, yleensä oma otsikko |
| `<aside>` | Sivusisältöön liittyvä mutta erillinen sisältö |
| `<footer>` | Sivun tai osion alatunniste |

Näiden käyttö pelkkien `<div>`-elementtien sijaan parantaa
saavutettavuutta (ruudunlukijat tunnistavat rakenteen) ja
hakukoneoptimointia.

## Tekstielementit

```html
<h1>Otsikko 1</h1> ... <h6>Otsikko 6</h6>   <!-- looginen hierarkia, ei hyppyjä -->
<p>Kappale</p>
<strong>Painotettu (semanttinen), yleensä lihavoituna</strong>
<em>Korostettu (semanttinen), yleensä kursiivilla</em>
<a href="https://esimerkki.fi">Linkki</a>
<br>  <!-- rivinvaihto tekstin sisällä -->
```

## Listat

```html
<ul>
  <li>Järjestämätön kohta</li>
</ul>

<ol>
  <li>Järjestetty kohta</li>
</ol>

<dl>
  <dt>Termi</dt>
  <dd>Termin selitys</dd>
</dl>
```

## Taulukot

```html
<table>
  <thead>
    <tr><th>Sarake 1</th><th>Sarake 2</th></tr>
  </thead>
  <tbody>
    <tr><td>Arvo A</td><td>Arvo B</td></tr>
  </tbody>
</table>
```

## Lomakkeet

```html
<form action="/lahetys" method="post">
  <label for="nimi">Nimi</label>
  <input type="text" id="nimi" name="nimi" required>

  <label for="email">Sähköposti</label>
  <input type="email" id="email" name="email">

  <select name="valinta">
    <option value="a">Vaihtoehto A</option>
  </select>

  <textarea name="viesti"></textarea>

  <button type="submit">Lähetä</button>
</form>
```
`<label for="...">` sidottuna `id`:hen on saavutettavuuden kannalta
tärkeä — ruudunlukija ja klikkaus kohdistuvat oikeaan kenttään.

## Kuvat ja media

```html
<img src="kuva.jpg" alt="Kuvan kuvaus" width="600" height="400">
<picture>
  <source srcset="kuva.webp" type="image/webp">
  <img src="kuva.jpg" alt="Kuvan kuvaus">
</picture>
<video src="video.mp4" controls></video>
```
`alt`-attribuutti on pakollinen saavutettavuuden vuoksi — kuvaile
kuvan sisältö, tai jätä tyhjäksi (`alt=""`) jos kuva on puhtaasti
koristeellinen.

## Semanttiset attribuutit

```html
<button aria-label="Sulje">×</button>
<div role="alert">Virheilmoitus</div>
<input aria-describedby="ohje-teksti">
<p id="ohje-teksti">Ohjeteksti kentälle</p>
```

## Kommentit

```html
<!-- Tämä ei näy sivulla -->
```
