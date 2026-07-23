---
title: Vimin lunttilappu
---

## Tilat

| Tila | Siirtyminen |
| --- | --- |
| Normaali | `Esc` |
| Lisäys (insert) | `i`, `a`, `o`, `O` |
| Visuaalinen | `v` (merkki), `V` (rivi), `Ctrl+V` (lohko) |
| Komento | `:` normaalitilassa |

## Liikkuminen

| Komento | Kuvaus |
| --- | --- |
| `h j k l` | Vasen / alas / ylös / oikea |
| `w` / `b` | Seuraavan / edellisen sanan alkuun |
| `0` / `$` | Rivin alkuun / loppuun |
| `gg` / `G` | Tiedoston alkuun / loppuun |
| `:<rivinumero>` | Siirry riville |

## Muokkaus

| Komento | Kuvaus |
| --- | --- |
| `dd` | Poista rivi |
| `yy` | Kopioi rivi |
| `p` / `P` | Liitä kopioidun jälkeen / eteen |
| `u` / `Ctrl+R` | Kumoa / tee uudelleen |
| `x` | Poista merkki |
| `cw` | Vaihda sana |
| `.` | Toista edellinen muutos |

## Haku ja korvaus

```
/haettava        " hae eteenpäin
?haettava        " hae taaksepäin
n / N            " seuraava / edellinen osuma
:%s/vanha/uusi/g " korvaa koko tiedostosta
```

## Tallennus ja poistuminen

```
:w      " tallenna
:q      " poistu
:wq     " tallenna ja poistu
:q!     " poistu tallentamatta
```
