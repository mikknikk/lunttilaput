---
title: Irssi
---

## Yhdistäminen

```
/connect irc.esimerkki.fi
/server add -auto -network Esimerkki irc.esimerkki.fi 6697
/network add -sasl_mechanism PLAIN -sasl_username nimi -sasl_password salasana Esimerkki
/connect Esimerkki
```

## Kanavat

| Komento | Kuvaus |
| --- | --- |
| `/join #kanava` | Liity kanavalle |
| `/part #kanava` | Poistu kanavalta |
| `/window close` | Sulje nykyinen ikkuna |
| `/names` | Listaa kanavan käyttäjät |
| `/topic` | Näytä kanavan aihe |
| `/topic uusi aihe` | Aseta kanavan aihe (jos oikeudet riittävät) |
| `/kick nimimerkki syy` | Poista käyttäjä kanavalta (operaattori) |
| `/mode #kanava +o nimimerkki` | Anna operaattorioikeudet |
| `/invite nimimerkki #kanava` | Kutsu käyttäjä kanavalle |

## Ikkunoiden hallinta

| Komento | Kuvaus |
| --- | --- |
| `Ctrl+N` / `Ctrl+P` | Seuraava / edellinen ikkuna |
| `Alt+<numero>` | Hyppää suoraan ikkunaan |
| `/window move <numero>` | Siirrä ikkuna toiseen paikkaan |
| `/window list` | Listaa kaikki ikkunat |
| `/layout save` | Tallenna ikkunoiden asettelu |
| `/split` | Jaa näyttö kahteen ikkunaan |
| `/window hide` / `/window show` | Piilota / näytä ikkuna jaetusta näkymästä |

## Yksityisviestit ja huomiot

```
/query nimimerkki
/msg nimimerkki viesti
/notify nimimerkki
/ignore nimimerkki ALL       " hiljennä käyttäjä kokonaan
/unignore nimimerkki
```

## Hälytykset (hilights)

```
/hilight sana
/hilight -color 4 oma-nimimerkki   " korosta oma nimi punaisella
/set beep_msg_level MSGS HILIGHT   " äänimerkki tietyistä tapahtumista
```

## Skriptit ja teemat

```
/script load skripti.pl
/script list
/set autoload_scripts skripti1 skripti2

/set theme oma-teema
```

Skriptejä ja teemoja löytyy irssin skriptiarkistosta (scripts.irssi.org).
Skriptit voivat lisätä esim. nimimerkkien värityksen tai away-ilmoitukset.

## Bouncer- ja proxy-käyttö

Irssi voidaan jättää pyörimään palvelimelle `screen`- tai `tmux`-istuntoon,
jotta yhteys pysyy yllä myös oman koneen ollessa pois päältä:

```bash
screen -S irssi irssi     # käynnistä irssi nimetyssä screen-istunnossa
screen -r irssi            # palaa istuntoon myöhemmin
```

## Lokit

```
/set autolog on
/set autolog_path ~/irclogs/$tag/$0.log
/set autolog_level all
```

## Muita hyödyllisiä asetuksia

```
/set nick uusi_nimimerkki
/set real_name "Oikea nimi"
/away Palaan pian
/away              " poista away-tila
/statusbar window add -after window lag   " näytä viive tilapalkissa
```
