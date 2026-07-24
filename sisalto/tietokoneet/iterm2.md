---
title: iTerm2
---

iTerm2 on macOS:n Terminal.appin korvaava sovellus: jaetut paneelit,
profiilit, hakutoiminnot, hotkey-ikkuna ja shell-integraatio komentojen
historiaan ja tilariviin.

## Välilehdet ja ikkunat

| Näppäin | Kuvaus |
| --- | --- |
| `Cmd+T` | Uusi välilehti |
| `Cmd+W` | Sulje nykyinen välilehti |
| `Cmd+<numero>` | Hyppää tiettyyn välilehteen |
| `Cmd+Left/Right` | Seuraava/edellinen välilehti |
| `` Cmd+` `` | Seuraava iTerm2-ikkuna |
| `Cmd+Enter` | Koko näytön tila päälle/pois |

## Jaetut paneelit (split panes)

| Näppäin | Kuvaus |
| --- | --- |
| `Cmd+D` | Jaa pystysuunnassa |
| `Cmd+Shift+D` | Jaa vaakasuunnassa |
| `Cmd+Option+Nuoli` | Siirry paneelien välillä sijainnin mukaan |
| `Cmd+]` / `Cmd+[` | Siirry paneelien välillä käyttöjärjestyksessä |
| `Ctrl+Cmd+Nuoli` | Muuta paneelin kokoa |
| `Cmd+Shift+Enter` | Suurenna nykyinen paneeli väliaikaisesti (sama näppäin palauttaa) |

Paneelin voi siirtää toiseen välilehteen hiiren oikealla painikkeella
("Move Session to Split Pane"), tai raahata hiirellä pitäen pohjassa
`Cmd+Option+Shift`.

## Hotkey-ikkuna

Preferences → Keys → Hotkey Window -asetuksesta voi rekisteröidä
näppäinyhdistelmän, joka tuo iTerm2:n aina näkyviin muusta sovelluksesta
riippumatta — samaan tapaan kuin Guake/Yakuake Linuxissa. Voidaan
asettaa avautumaan omana pudotusikkunanaan (dedicated hotkey window).

## Broadcast Input — sama komento useaan paneeliin

```
Cmd+Option+I    " ota käyttöön/pois broadcast-tila
```
Kun tila on päällä, kirjoitettu teksti lähetetään kaikkiin saman
välilehden paneeleihin samanaikaisesti — kätevää, kun samaa komentoa
ajetaan useammalle palvelimelle rinnakkain.

## Ikkuna-asettelun tallennus

```
Window → Save Window Arrangement
Window → Restore Window Arrangement
```
Voidaan myös asettaa palautumaan automaattisesti käynnistyksessä
(Preferences → General).

## Shell-integraatio

Asennetaan lisäämällä lataussivun antama rivi shellin profiilitiedostoon
(esim. `~/.zshrc`). Mahdollistaa mm. komentohistorian merkinnät
vierityspalkissa, tilarivi-integraation ja parannetun istunnonhallinnan.

## Modifier-näppäinten uudelleenmääritys

Preferences → Keys → Remap Modifier Keys — esim. Option- ja
Cmd-näppäinten vaihtaminen keskenään, jos oletussijoittelu ei sovi omaan
näppäimistöön.

## Haku istunnossa

```
Cmd+F
```
Etsii nykyisen paneelin näkyvästä ja vieritettävästä historiasta.
