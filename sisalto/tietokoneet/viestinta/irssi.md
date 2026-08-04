---
title: Irssi
---

## Yhdistäminen

```
/connect irc.esimerkki.fi
/server add -auto -network Esimerkki -tls irc.esimerkki.fi 6697
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
| `/window new split` | Jaa näyttö kahteen ikkunaan |

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

### Hyödyllisiä skriptejä

| Skripti | Kuvaus |
| --- | --- |
| `nickcolor.pl` | Antaa jokaiselle nimimerkille oman värin — helpottaa keskustelun seuraamista vilkkailla kanavilla |
| `adv_windowlist.pl` | Näyttää ikkunalistassa kanavien/nimimerkkien oikeat nimet pelkkien numeroiden sijaan |
| `trackbar.pl` | Piirtää viivan kohtaan, josta viimeksi jäit lukemasta, kun vaihdat ikkunaa |
| `screen_away.pl` | Päivittää away-tilan automaattisesti, kun irssi pyörii `screen`/`tmux`-istunnossa |
| `go.pl` | `/go`-komento älykkäällä täydennyksellä ikkunoiden väliseen hyppäämiseen |
| `hilightwin.pl` | Kerää kaikki hälytykset (highlight) omaan, esim. jaettuun ikkunaan |
| `spell.pl` | Oikeinkirjoituksen tarkistus (vaatii `ispell`-asennuksen) |
| `trigger.pl` | Yleiskäyttöinen "kun X tapahtuu, tee Y" -automaatio |

```
/script load nickcolor.pl
/script load adv_windowlist.pl
/script load trackbar.pl
```

## Skriptien poisto (uninstallointi)

Skriptin poistaminen on kaksivaiheinen: sen pysäyttäminen nykyisestä
istunnosta ja sen estäminen lataamasta uudelleen jatkossa.

```
/script unload skripti      " pysäytä skripti nykyisessä istunnossa (ei tarvitse .pl-päätettä)
/script list                  " tarkista että se ei enää näy listalla
```

Pelkkä `/script unload` ei estä skriptiä latautumasta uudelleen
seuraavalla käynnistyskerralla, jos se on asetettu automaattisesti
ladattavaksi. Poista automaattilataus sen mukaan, kumpaa tapaa käytit
käyttöönotossa:

```bash
# Jos skripti on ladattu autorun-kansion symlinkillä (suositeltu tapa):
rm ~/.irssi/scripts/autorun/skripti.pl
```

```
# Jos skripti on listattu autoload_scripts-asetuksessa:
/set autoload_scripts skripti1 skripti2   " kirjoita lista ilman poistettavaa skriptiä
```

Lopuksi, jos haluat poistaa skriptin kokonaan levyltä (ei vain
käytöstä):

```bash
rm ~/.irssi/scripts/skripti.pl
```
Pelkkä autorun-symlinkin poisto riittää, jos haluat vain lopettaa sen
automaattilatauksen mutta säilyttää tiedoston mahdollista myöhempää
`/script load`-komentoa varten.

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
