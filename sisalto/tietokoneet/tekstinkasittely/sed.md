---
title: Sed
---

sed (stream editor) muokkaa tekstiä rivi kerrallaan komentojonon
perusteella — ei vaadi tiedoston avaamista editorissa.

## Perusmuoto (korvaus)

```bash
sed 's/vanha/uusi/' tiedosto            # korvaa ensimmäisen osuman jokaisella rivillä
sed 's/vanha/uusi/g' tiedosto            # korvaa kaikki osumat joka rivillä (global)
sed 's/vanha/uusi/gi' tiedosto             # korvaa, ei väliä kirjainkoolla
sed 's/vanha/uusi/2' tiedosto               # korvaa vain rivin 2. osuma
komento | sed 's/vanha/uusi/g'                # putkessa
```

## Paikallaan muokkaus (`-i`)

```bash
sed -i 's/vanha/uusi/g' tiedosto            # GNU sed (Linux)
sed -i '' 's/vanha/uusi/g' tiedosto           # BSD sed (macOS) — vaatii tyhjän varmuuskopiopäätteen argumentin
sed -i.bak 's/vanha/uusi/g' tiedosto            # molemmat: tekee varmuuskopion tiedosto.bak
```
**Tämä on yleisin sudenkuoppa macOS:lla:** BSD sed vaatii `-i`:n jälkeen
aina jonkin argumentin (vaikka tyhjän `''`), GNU sed ei. Ilman tätä eroa
komento joko epäonnistuu tai luo vahingossa tiedoston nimeltä `s`.

## Osoitteet (mille riveille komento kohdistuu)

```bash
sed '3s/vanha/uusi/' tiedosto           # vain rivi 3
sed '2,5s/vanha/uusi/' tiedosto           # rivit 2–5
sed '/aloitus/,/lopetus/s/vanha/uusi/' tiedosto   # rivien "aloitus" ja "lopetus" välissä
sed '$s/vanha/uusi/' tiedosto              # vain viimeinen rivi
sed -n '3,5p' tiedosto                       # tulosta vain rivit 3–5 (-n hiljentää oletustulostuksen)
```

## Rivien poisto

```bash
sed '3d' tiedosto             # poista rivi 3
sed '2,5d' tiedosto             # poista rivit 2–5
sed '/^#/d' tiedosto              # poista kommenttirivit (alkavat #:llä)
sed '/^$/d' tiedosto                # poista tyhjät rivit
```

## Capture-ryhmät ja takaisinviittaukset

```bash
sed -E 's/([a-z]+)@([a-z]+)/\2@\1/' tiedosto   # vaihda @-merkin ympärillä olevat osat keskenään
sed 's/.*/[&]/' tiedosto                          # & viittaa koko täsmäävään osuun
```
`-E` (tai `-r` GNU sed:issä) ottaa käyttöön laajennetun regexin, jolloin
`()`- ja `+`-merkkejä ei tarvitse erikseen escapoida `\`:lla.

## Useampi komento

```bash
sed -e 's/a/b/' -e 's/c/d/' tiedosto
sed 's/a/b/; s/c/d/' tiedosto     # sama, puolipisteellä eroteltuna
```

## Yleisiä käytännön esimerkkejä

```bash
sed -n '10,20p' loki.txt                  # näytä vain rivit 10–20
grep -rl "vanha" . | xargs sed -i 's/vanha/uusi/g'   # korvaa kaikissa hakemiston tiedostoissa
sed 's/[[:space:]]*$//' tiedosto            # poista rivien lopusta ylimääräiset välilyönnit
sed = tiedosto | sed 'N;s/\n/\t/'             # numeroi rivit
```

## sed vs. muokkaus editorissa

sed sopii kertaluontoisiin, skriptattaviin tai massamuokkauksiin
(esim. saman muutoksen tekeminen sadalle tiedostolle CI-liukuhihnassa) —
interaktiiviseen, harkinnanvaraiseen muokkaukseen sopii paremmin
tavallinen editori (ks. Vim- tai Nano-lunttilappu).
