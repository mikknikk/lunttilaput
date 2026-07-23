---
title: Awkin lunttilappu
---

## Perusmuoto

```bash
awk '{ print }' tiedosto          # tulosta jokainen rivi
awk '{ print $1 }' tiedosto       # tulosta ensimmäinen kenttä
awk -F: '{ print $1 }' /etc/passwd  # kenttäerotin ":"
```

## Sisäänrakennetut muuttujat

| Muuttuja | Kuvaus |
| --- | --- |
| `$0` | Koko nykyinen rivi |
| `$1`, `$2`, ... | Rivin kentät järjestyksessä |
| `NF` | Kenttien lukumäärä rivillä |
| `NR` | Nykyisen rivin numero |
| `FS` | Kenttäerotin (oletus: välilyönti) |
| `OFS` | Tulosteen kenttäerotin |

## Ehdot ja suodatus

```bash
awk '$3 > 100 { print $1 }' data.txt      # rivit, joilla 3. kenttä > 100
awk '/virhe/ { print }' loki.txt          # rivit, jotka täsmäävät regexiin
awk 'NR == 1' tiedosto                    # vain ensimmäinen rivi
awk 'NF > 0' tiedosto                     # ohita tyhjät rivit
```

## Laskenta

```bash
awk '{ summa += $1 } END { print summa }' luvut.txt
awk 'END { print NR }' tiedosto           # rivien lukumäärä
```

## Kentän erottimen vaihto tulosteessa

```bash
awk 'BEGIN { OFS="," } { print $1, $2 }' tiedosto
```
