---
title: Bash
---

## Muuttujat

```bash
nimi="arvo"
echo "$nimi"
export POLKU="/usr/local/bin"   # vie ympäristöön aliprosesseille
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
```

## Silmukat

```bash
for tiedosto in *.txt; do
  echo "$tiedosto"
done

while read -r rivi; do
  echo "$rivi"
done < tiedosto.txt
```

## Putket ja uudelleenohjaukset

| Merkintä | Kuvaus |
| --- | --- |
| `komento1 \| komento2` | Putki: ensimmäisen tuloste toisen syötteeksi |
| `>` | Ohjaa tuloste tiedostoon (ylikirjoittaa) |
| `>>` | Ohjaa tuloste tiedoston loppuun |
| `2>&1` | Ohjaa virheet samaan paikkaan kuin tuloste |
| `<` | Lue syöte tiedostosta |

## Hyödyllisiä pikanäppäimiä

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+R` | Hae komentohistoriasta |
| `Ctrl+A` / `Ctrl+E` | Rivin alkuun / loppuun |
| `Ctrl+U` / `Ctrl+K` | Poista kursorista rivin alkuun / loppuun |
| `!!` | Toista edellinen komento |
| `!$` | Edellisen komennon viimeinen argumentti |

## Funktiot

```bash
tervehdi() {
  echo "Hei, $1!"
}
tervehdi "maailma"
```
