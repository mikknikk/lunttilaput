---
title: Bash
---

## Muuttujat

```bash
nimi="arvo"
echo "$nimi"
export POLKU="/usr/local/bin"   # vie ympäristöön aliprosesseille
readonly VAKIO="ei muutu"
unset nimi
```

## Parametrilaajennus

```bash
echo "${nimi:-oletus}"     # käytä "oletus", jos nimi on tyhjä/olematon
echo "${nimi:=oletus}"     # sama, mutta myös ASETTAA nimen
echo "${nimi:?virhe}"      # keskeytä virheellä, jos tyhjä
echo "${nimi#etu}"          # poista lyhin täsmäävä etuliite
echo "${nimi%loppu}"        # poista lyhin täsmäävä loppuliite
echo "${nimi//vanha/uusi}"  # korvaa kaikki osumat
echo "${#nimi}"             # merkkijonon pituus
```

## Taulukot

```bash
taulukko=(eka toka kolmas)
echo "${taulukko[0]}"       # eka
echo "${taulukko[@]}"       # kaikki alkiot
echo "${#taulukko[@]}"      # alkioiden lukumäärä
taulukko+=(neljäs)          # lisää alkio

for alkio in "${taulukko[@]}"; do
  echo "$alkio"
done
```

## Ehtolauseet

```bash
if [ -f tiedosto ]; then
  echo "on olemassa"
elif [ -d kansio ]; then
  echo "on kansio"
else
  echo "ei kumpaakaan"
fi

# [[ ]] tukee mm. regexiä ja on turvallisempi lainausmerkkien suhteen
if [[ "$nimi" =~ ^[0-9]+$ ]]; then
  echo "pelkkiä numeroita"
fi

case "$nimi" in
  alku*) echo "alkaa alulla" ;;
  *loppu) echo "päättyy loppuun" ;;
  *) echo "muu" ;;
esac
```

## Silmukat

```bash
for tiedosto in *.txt; do
  echo "$tiedosto"
done

for i in {1..5}; do
  echo "$i"
done

while read -r rivi; do
  echo "$rivi"
done < tiedosto.txt

until [ "$valmis" = "kylla" ]; do
  read -r valmis
done
```

## Putket ja uudelleenohjaukset

| Merkintä | Kuvaus |
| --- | --- |
| `komento1 \| komento2` | Putki: ensimmäisen tuloste toisen syötteeksi |
| `>` | Ohjaa tuloste tiedostoon (ylikirjoittaa) |
| `>>` | Ohjaa tuloste tiedoston loppuun |
| `2>&1` | Ohjaa virheet samaan paikkaan kuin tuloste |
| `2>` | Ohjaa vain virheet tiedostoon |
| `<` | Lue syöte tiedostosta |
| `<<EOF` | Here-document: monirivinen syöte suoraan skriptiin |
| `<(komento)` | Prosessikorvaus: käsittele komennon tuloste kuin tiedostoa |

```bash
diff <(sort a.txt) <(sort b.txt)

cat <<EOF > viesti.txt
Rivi 1
Rivi 2
EOF
```

## Funktiot

```bash
tervehdi() {
  local nimi="$1"          # local rajaa muuttujan funktion sisälle
  echo "Hei, $nimi!"
  return 0
}
tervehdi "maailma"
```

## Poistumiskoodit ja virheenkäsittely

```bash
komento
echo $?                   # edellisen komennon poistumiskoodi (0 = onnistui)

set -euo pipefail         # keskeytä virheeseen, tuntemattomaan muuttujaan
                           # tai putken sisäiseen virheeseen
trap 'echo "Keskeytetty"; exit 1' INT TERM
```

## Prosessit ja työnhallinta

```bash
komento &          # aja taustalla
jobs                # listaa taustatyöt
fg %1               # tuo työ 1 etualalle
kill %1             # lopeta taustatyö
wait                # odota kaikkien taustatöiden valmistumista
```

## Hyödyllisiä pikanäppäimiä

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+R` | Hae komentohistoriasta |
| `Ctrl+A` / `Ctrl+E` | Rivin alkuun / loppuun |
| `Ctrl+U` / `Ctrl+K` | Poista kursorista rivin alkuun / loppuun |
| `Ctrl+W` | Poista edellinen sana |
| `Ctrl+L` | Tyhjennä näyttö |
| `Ctrl+C` / `Ctrl+Z` | Keskeytä / pysäytä prosessi |
| `!!` | Toista edellinen komento |
| `!$` | Edellisen komennon viimeinen argumentti |
| `!nimi` | Toista viimeisin komento, joka alkoi "nimi" |

## Alias ja skriptin alku

```bash
alias ll='ls -la'

#!/usr/bin/env bash
set -euo pipefail
```
