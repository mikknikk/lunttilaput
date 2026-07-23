---
title: Grep
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
| `-r` / `-R` | Rekursiivinen haku hakemistopuussa (`-R` seuraa symlinkkejä) |
| `-n` | Näytä rivinumero |
| `-c` | Näytä vain osumien lukumäärä |
| `-l` | Näytä vain tiedostonimet, joissa osuma |
| `-L` | Näytä tiedostonimet, joissa EI osumaa |
| `-w` | Vaadi koko sana |
| `-x` | Vaadi koko rivin täsmäys |
| `-o` | Tulosta vain täsmäävä osa, ei koko riviä |
| `-A n` / `-B n` | Näytä n riviä osuman jälkeen / ennen |
| `-C n` | Näytä n riviä molemmin puolin |
| `-E` | Laajennettu regex (sama kuin `egrep`) |
| `-F` | Kirjaimellinen merkkijonohaku, ei regexiä (sama kuin `fgrep`) |
| `-e` | Anna useampi hakulauseke |
| `-q` | Hiljainen: käytä vain poistumiskoodia (skripteissä) |

## Esimerkkejä

```bash
grep -rn "TODO" src/                  # etsi TODO-kommentit rekursiivisesti
grep -riL "copyright" *.md            # tiedostot, joista puuttuu sana
grep -E "virhe|error" loki.txt        # useampi vaihtoehto kerralla
ps aux | grep -i python               # käynnissä olevat python-prosessit
grep -c "^#" tiedosto.py              # kommenttirivien määrä
grep -o "IP: [0-9.]*" loki.txt        # poimi vain osumat, ei koko riviä
grep -rl "vanha-nimi" . | xargs sed -i 's/vanha-nimi/uusi-nimi/g'
grep --include="*.py" -rn "import os" .   # rajaa tiedostotyyppiin
grep --exclude-dir=node_modules -rn "TODO" .
```

## Useampi hakulauseke

```bash
grep -e "virhe" -e "varoitus" loki.txt
grep -f haut.txt tiedosto              # hakulausekkeet tiedostosta, rivi kerrallaan
```

## Regex-perusteet grepissä

| Merkki | Kuvaus |
| --- | --- |
| `.` | Mikä tahansa merkki |
| `*` | Edellinen merkki 0-n kertaa |
| `+` (vain `-E`:llä) | Edellinen merkki 1-n kertaa |
| `?` (vain `-E`:llä) | Edellinen merkki 0-1 kertaa |
| `^` / `$` | Rivin alku / loppu |
| `[abc]` | Jokin merkeistä a, b, c |
| `[^abc]` | Mikä tahansa muu kuin a, b, c |
| `[0-9]` | Numeroalue |
| `\d`, `\w`, `\s` | (vain `-P`:llä) numero, sana- tai tyhjämerkki |
| `\|` (vain `-E`:llä) | Vaihtoehto |
| `{n,m}` (vain `-E`:llä) | Toistokerrat n-m |

## PCRE (Perl-yhteensopiva regex)

```bash
grep -P "(?<=IP: )\d+\.\d+\.\d+\.\d+" loki.txt   # katsomaehto (lookbehind)
```
`-P` ei ole saatavilla kaikissa grep-toteutuksissa (esim. macOS:n
oletus-BSD-grepistä puuttuu — asenna tarvittaessa GNU grep: `brew install grep`).

## Pakatut tiedostot

```bash
zgrep "haettava" loki.gz     # hae pakatusta tiedostosta purkamatta sitä ensin
```
