---
title: Nano
---

## Avaaminen

```bash
nano tiedosto.txt
nano +42 tiedosto.txt      # avaa suoraan riville 42
nano +42,5 tiedosto.txt    # rivi 42, sarake 5
nano -B tiedosto.txt       # tee varmuuskopio ennen tallennusta
```

Nanon alareunassa näkyvät komennot: `^` tarkoittaa `Ctrl`, `M-` tarkoittaa `Alt`/`Esc`.

## Tallennus ja poistuminen

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+O` | Tallenna (Write Out) |
| `Ctrl+X` | Poistu (kysyy tallennusta jos muutoksia) |
| `Ctrl+C` | Näytä kursorin sijainti |
| `Ctrl+T` | Tarkista oikeinkirjoitus (jos asennettu) |

## Muokkaus

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+K` | Leikkaa rivi |
| `Ctrl+U` | Liitä leikattu rivi |
| `Ctrl+Shift+6` tai `Alt+A` | Aloita merkintä (valinta) |
| `Ctrl+6` | Kopioi valinta |
| `Alt+6` | Leikkaa valinta |
| `Ctrl+Z` | Kumoa |
| `Ctrl+Shift+Z` tai `M-U` | Tee uudelleen |
| `Tab` / `Shift+Tab` | Sisennä / poista sisennys (valinnalle) |
| `Alt+3` | Kommentoi/poista kommentti rivi(t) |

## Haku ja korvaus

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+W` | Hae |
| `Ctrl+\` | Hae ja korvaa |
| `Alt+W` | Hae seuraava osuma |
| `Alt+Q` | Hae edellinen osuma |
| `Alt+R` (haun aikana) | Vaihda tavallisen haun ja regex-haun välillä |

## Liikkuminen

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+A` / `Ctrl+E` | Rivin alkuun / loppuun |
| `Ctrl+Y` / `Ctrl+V` | Sivu ylös / alas |
| `Alt+G` | Siirry tietylle riville |
| `Ctrl+Left` / `Ctrl+Right` | Sana taaksepäin / eteenpäin |
| `Alt+\` / `Alt+/` | Tiedoston alkuun / loppuun |

## Useampi tiedosto (välilehdet/puskurit)

```bash
nano -F tiedosto1.txt tiedosto2.txt   # avaa useampi tiedosto kerralla
```

| Näppäin | Kuvaus |
| --- | --- |
| `Alt+<` / `Alt+>` | Edellinen / seuraava avoin puskuri |
| `Ctrl+R` | Liitä toisen tiedoston sisältö nykyiseen kohtaan |

## Rivinumerot ja syntaksikorostus

```bash
nano -l tiedosto.py    # näytä rivinumerot
```

Syntaksikorostus tulee yleensä mukana jakelun `/usr/share/nano/`-tiedostoista
automaattisesti tiedostopäätteen perusteella.

## Asetustiedosto `~/.nanorc`

```
set linenumbers
set autoindent
set tabsize 4
set mouse
include "/usr/share/nano/*.nanorc"
```
