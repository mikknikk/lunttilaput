---
title: Grepin lunttilappu
---

## Perusmuoto

```bash
grep "haettava" tiedosto
grep "haettava" *.txt
komento | grep "haettava"
```

## Yleisiä valitsimia

| Valitsin | Kuvaus |
| --- | --- |
| `-i` | Ei väliä kirjainkoolla |
| `-v` | Käänteinen haku (rivit, joilla EI osumaa) |
| `-r` / `-R` | Rekursiivinen haku hakemistopuussa |
| `-n` | Näytä rivinumero |
| `-c` | Näytä vain osumien lukumäärä |
| `-l` | Näytä vain tiedostonimet, joissa osuma |
| `-w` | Vaadi koko sana |
| `-A n` / `-B n` | Näytä n riviä osuman jälkeen / ennen |
| `-E` | Laajennettu regex (sama kuin `egrep`) |

## Esimerkkejä

```bash
grep -rn "TODO" src/                  # etsi TODO-kommentit rekursiivisesti
grep -riL "copyright" *.md            # tiedostot, joista puuttuu sana
grep -E "virhe|error" loki.txt        # useampi vaihtoehto kerralla
ps aux | grep -i python               # käynnissä olevat python-prosessit
grep -c "^#" tiedosto.py              # kommenttirivien määrä
```

## Regex-perusteet grepissä

| Merkki | Kuvaus |
| --- | --- |
| `.` | Mikä tahansa merkki |
| `*` | Edellinen merkki 0-n kertaa |
| `^` / `$` | Rivin alku / loppu |
| `[abc]` | Jokin merkeistä a, b, c |
| `\|` (vain `-E`:llä) | Vaihtoehto |
