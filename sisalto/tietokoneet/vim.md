---
title: Vim
---

## Tilat

| Tila | Siirtyminen |
| --- | --- |
| Normaali | `Esc` |
| Lisäys (insert) | `i`, `a`, `o`, `O` |
| Visuaalinen | `v` (merkki), `V` (rivi), `Ctrl+V` (lohko) |
| Komento | `:` normaalitilassa |
| Korvaus (replace) | `R` |

## Liikkuminen

| Komento | Kuvaus |
| --- | --- |
| `h j k l` | Vasen / alas / ylös / oikea |
| `w` / `b` | Seuraavan / edellisen sanan alkuun |
| `e` | Seuraavan sanan loppuun |
| `0` / `$` | Rivin alkuun / loppuun |
| `^` | Rivin ensimmäiseen ei-tyhjään merkkiin |
| `gg` / `G` | Tiedoston alkuun / loppuun |
| `:<rivinumero>` tai `<rivinumero>G` | Siirry riville |
| `%` | Hyppää täsmäävään sulkuun `()`, `{}`, `[]` |
| `Ctrl+O` / `Ctrl+I` | Edellinen / seuraava sijainti hyppyhistoriassa |

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
| `dw`, `d$`, `dG` | Poista sanaan/rivin loppuun/tiedoston loppuun asti |
| `>>` / `<<` | Sisennä / poista sisennys |
| `J` | Yhdistä seuraava rivi nykyiseen |
| `~` | Vaihda merkin kirjainkoko |

## Rekisterit ja merkit

```
"ayy      " kopioi rivi rekisteriin a
"ap       " liitä rekisterin a sisältö
ma        " aseta merkki "a" nykyiseen sijaintiin
`a        " hyppää merkkiin "a"
```
Rekisterit mahdollistavat useamman leikkauksen/kopion pitämisen samanaikaisesti.

## Makrot

```
qa        " aloita makron tallennus rekisteriin a
...       " tehdyt komennot tallentuvat
q         " lopeta tallennus
@a        " toista makro a
@@        " toista viimeisin makro uudelleen
5@a       " toista makro a viisi kertaa
```

## Haku ja korvaus

```
/haettava        " hae eteenpäin
?haettava        " hae taaksepäin
n / N            " seuraava / edellinen osuma
:%s/vanha/uusi/g " korvaa koko tiedostosta
:%s/vanha/uusi/gc " korvaa vahvistaen jokaisen kohdalla
:5,10s/vanha/uusi/g " korvaa vain riveillä 5-10
```

## Ikkunat ja välilehdet

```
:split            " jaa ikkuna vaakasuunnassa
:vsplit           " jaa ikkuna pystysuunnassa
Ctrl+W w          " vaihda ikkunoiden välillä
Ctrl+W q          " sulje nykyinen ikkuna
:tabnew tiedosto  " avaa tiedosto uuteen välilehteen
gt / gT           " seuraava / edellinen välilehti
```

## Taittaminen (folding)

```
zf}       " luo taite kappaleen ympärille
za        " avaa/sulje taite kursorin kohdalla
zR        " avaa kaikki taitteet
zM        " sulje kaikki taitteet
```

## Tallennus ja poistuminen

```
:w      " tallenna
:w tiedostonimi " tallenna toisella nimellä
:q      " poistu
:wq     " tallenna ja poistu
:q!     " poistu tallentamatta
:x      " tallenna vain jos muutoksia, ja poistu
```

## Perusasetukset (`~/.vimrc`)

```vim
set number          " näytä rivinumerot
set expandtab       " käytä välilyöntejä sarkaimen sijaan
set shiftwidth=2
set incsearch       " näytä osumat jo kirjoitettaessa
syntax on
```
