---
title: GIMP
---

GIMP (GNU Image Manipulation Program) on ilmainen, avoimen lähdekoodin
kuvankäsittelyohjelma — vapaa vaihtoehto esim. Photoshopille. GIMP 3.0
(2025) siirsi ohjelman modernille GTK3-pohjalle (parempi HiDPI-, Wayland-
ja tablettituki), ja GIMP 3.2 (maaliskuu 2026) toi mukanaan mm.
tuhoamattomat (non-destructive) linkitetyt kuvatasot.

## Tallennus vs. vienti — yleisin sekaannuksen aihe

| Näppäin | Toiminto |
| --- | --- |
| `Ctrl+S` | Tallenna GIMPin omaan `.xcf`-muotoon (tasot, historia säilyvät) |
| `Ctrl+Shift+E` | Vie (Export As) esim. PNG/JPG-muotoon |
| `Ctrl+E` | Vie uudelleen samaan tiedostoon/muotoon kuin viimeksi |

**Huom:** `Ctrl+S` ei koskaan tallenna suoraan PNG:ksi tai JPG:ksi —
vain `.xcf`:ksi. Muihin muotoihin viedään aina erikseen `Export
As`-komennolla, ja alkuperäinen muokattavuus (tasot ym.) säilyy vain
`.xcf`-tiedostossa.

## Työkalut (yksittäiset pikanäppäimet)

| Näppäin | Työkalu |
| --- | --- |
| `M` | Siirrä (Move) |
| `R` | Suorakulmiovalinta |
| `E` | Ellipsivalinta |
| `F` | Vapaa valinta (lasso) |
| `U` | Sumea valinta (taikasauva) |
| `Shift+O` | Valitse värin mukaan |
| `P` | Siveltimet (Paintbrush) |
| `N` | Kynä (Pencil) |
| `Shift+E` | Pyyhekumi |
| `Shift+B` | Täyttö (Bucket fill) |
| `L` | Liuku/gradientti (Blend) |
| `C` | Kloonaustyökalu |
| `H` | Korjaussivellin (Heal) |
| `S` | Sormella sively (Smudge) |
| `Shift+D` | Varjosta/vaalenna (Dodge/Burn) |
| `T` | Teksti |
| `B` | Polku (Path) |
| `O` | Väripipetti |
| `Z` | Zoomaus |

## Valinnat

```
Shift+Ctrl+A     " poista valinta (Select None)
Shift+Q            " Quick Mask päälle/pois — maalaa valinta siveltimellä
```
Quick Mask on erittäin hyödyllinen tarkkojen, epäsäännöllisten
valintojen tekemiseen — valinta muutetaan väliaikaisesti punaiseksi
peittokerrokseksi, jota voi maalata tavallisilla sivellintyökaluilla.

**Huom:** `Ctrl+D` ei toista viimeistä valintaa kuten monessa muussa
ohjelmassa — se **kopioi koko kuvan** uuteen ikkunaan.

## Tasot (layers)

```
Ctrl+Shift+N     " uusi taso
Ctrl+Shift+D       " kopioi aktiivinen taso
Ctrl+Shift+C         " kopioi kaikkien näkyvien tasojen yhdistelmä (ilman että itse tasot yhdistyvät pysyvästi)
```
GIMP 3.0:sta lähtien useamman tason voi valita samanaikaisesti
(monivalinta) ja siirtää/muuntaa/nimetä ryhmänä — aiemmissa versioissa
tämä ei ollut mahdollista.

## Muunnostyökalut

| Näppäin | Työkalu |
| --- | --- |
| `Shift+T` | Skaalaus |
| `Shift+C` | Rajaus (Crop) |
| `Shift+W` | 3D-muunnos (GIMP 3.x) |
| `Shift+L` | Handle-muunnos (GIMP 3.x) |
| `Shift+G` | Cage-muunnos (GIMP 3.x) |

## Ikkunan/näkymän hallinta

```
Ctrl+J           " sovita ikkuna kuvan kokoon (Shrink Wrap)
Shift+Ctrl+J       " sovita kuva ikkunaan (Fit Image in Window)
```

## Automaatio: Script-Fu

```
Filters → Script-Fu → Console
```
Script-Fu-konsoli mahdollistaa GIMPin ohjaamisen Scheme-pohjaisilla
skripteillä — hyödyllinen esim. saman muokkauksen toistamiseen
kymmenille/sadoille kuville kerralla (eräajo).

## GIMP 3.x:n keskeisimmät uudistukset

- **GTK3-pohja:** parempi HiDPI-, Wayland- ja tablettituki, sekä
  automaattinen tumma/vaalea tila käyttöjärjestelmän mukaan (3.2).
- **Tuhoamattomat linkitetyt kuvatasot ja vektoritasot (3.2):**
  ulkoisen kuvan voi linkittää tasoksi ilman että sen alkuperäinen laatu
  kärsii skaalauksesta/kierrosta, ja muodot pysyvät muokattavina
  (täyttö/reunaviiva) sen sijaan että rasteroituisivat heti.
- **Monivalinta tasoille:** ks. Tasot-osio yllä.
