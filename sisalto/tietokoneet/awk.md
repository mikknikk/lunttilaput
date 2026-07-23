---
title: Awk
---

## Perusmuoto

```bash
awk '{ print }' tiedosto          # tulosta jokainen rivi
awk '{ print $1 }' tiedosto       # tulosta ensimmäinen kenttä
awk -F: '{ print $1 }' /etc/passwd  # kenttäerotin ":"
awk -f skripti.awk tiedosto        # ohjelma tiedostosta
```

## Sisäänrakennetut muuttujat

| Muuttuja | Kuvaus |
| --- | --- |
| `$0` | Koko nykyinen rivi |
| `$1`, `$2`, ... | Rivin kentät järjestyksessä |
| `NF` | Kenttien lukumäärä rivillä |
| `NR` | Nykyisen rivin numero (kaikkien tiedostojen yli) |
| `FNR` | Rivin numero nykyisessä tiedostossa |
| `FS` | Kenttäerotin (oletus: välilyönti/tabulaattori) |
| `OFS` | Tulosteen kenttäerotin |
| `RS` | Tietueen (rivin) erotin |
| `ORS` | Tulosteen tietueen erotin |
| `FILENAME` | Käsiteltävän tiedoston nimi |

## Ohjelman rakenne

```bash
awk 'BEGIN { print "Alussa" }
     { print "Joka rivillä:", $0 }
     END { print "Lopussa" }' tiedosto
```

`BEGIN` suoritetaan ennen syötteen lukua, pääosa jokaiselle riville, `END`
kun kaikki on luettu.

## Ehdot ja suodatus

```bash
awk '$3 > 100 { print $1 }' data.txt      # rivit, joilla 3. kenttä > 100
awk '/virhe/ { print }' loki.txt          # rivit, jotka täsmäävät regexiin
awk '$2 ~ /^A/ { print }' data.txt        # 2. kenttä alkaa kirjaimella A
awk 'NR == 1' tiedosto                    # vain ensimmäinen rivi
awk 'NR > 1' tiedosto                     # ohita otsikkorivi
awk 'NF > 0' tiedosto                     # ohita tyhjät rivit
awk '$1 == "virhe" || $1 == "varoitus"' loki.txt
```

## Laskenta ja koonti

```bash
awk '{ summa += $1 } END { print summa }' luvut.txt
awk '{ summa += $1; n++ } END { print summa/n }' luvut.txt   # keskiarvo
awk 'max == "" || $1 > max { max = $1 } END { print max }' luvut.txt
awk 'END { print NR }' tiedosto           # rivien lukumäärä
```

## Taulukot (assosiatiiviset)

```bash
# Laske sanojen esiintymät
awk '{ for (i=1; i<=NF; i++) count[$i]++ }
     END { for (sana in count) print sana, count[sana] }' teksti.txt

# Ryhmittely toisen kentän mukaan
awk -F, '{ summa[$2] += $3 } END { for (k in summa) print k, summa[k] }' data.csv
```

## Merkkijonofunktiot

| Funktio | Kuvaus |
| --- | --- |
| `length($0)` | Merkkijonon/rivin pituus |
| `substr(s, alku, pituus)` | Osamerkkijono |
| `toupper(s)` / `tolower(s)` | Iso/pieni kirjainkoko |
| `split(s, arr, erotin)` | Pilko merkkijono taulukkoon |
| `gsub(regex, korvaus, s)` | Korvaa kaikki osumat |
| `sub(regex, korvaus, s)` | Korvaa ensimmäinen osuma |
| `sprintf(fmt, ...)` | Muotoile merkkijono |

## Omat funktiot

```bash
awk '
function nelio(x) { return x * x }
{ print nelio($1) }
' luvut.txt
```

Käytä funktioiden nimissä pelkkiä ASCII-kirjaimia (ei ä/ö/å) — monet
awk-toteutukset (mm. mawk, alkuperäinen awk) eivät hyväksy muita kuin
ASCII-merkkejä tunnisteissa, joten esim. `neliö` voi aiheuttaa
syntaksivirheen.

## Tulosteen muotoilu

```bash
awk '{ printf "%-10s %5d\n", $1, $2 }' tiedosto   # sarakkeistettu tuloste
awk 'BEGIN { OFS="," } { print $1, $2 }' tiedosto  # vaihda kenttäerotin
```

## Useampi tiedosto ja rivin erotin

```bash
awk '{ print FILENAME, NR, $0 }' a.txt b.txt   # tiedostonimi + globaali rivinumero
awk 'BEGIN { RS="" ; FS="\n" } { print $1 }' tiedosto   # kappaleet tietueina
```
