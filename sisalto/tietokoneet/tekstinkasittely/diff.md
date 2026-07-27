---
title: Diff
---

`diff` vertailee kahta tiedostoa (tai hakemistoa) ja näyttää niiden erot.

## Peruskäyttö

```bash
diff tiedosto1.txt tiedosto2.txt
diff -u tiedosto1.txt tiedosto2.txt     # unified diff — yleisin, patchien/gitin käyttämä muoto
diff -c tiedosto1.txt tiedosto2.txt      # context diff — enemmän ympäröivää kontekstia
diff -y tiedosto1.txt tiedosto2.txt        # rinnakkainen (side-by-side) näkymä
```

## Unified diff -muodon lukeminen (`-u`)

```diff
--- tiedosto1.txt	2026-01-01
+++ tiedosto2.txt	2026-01-02
@@ -1,4 +1,4 @@
 Muuttumaton rivi
-Poistettu rivi
+Lisätty rivi
 Toinen muuttumaton rivi
```

| Merkki | Kuvaus |
| --- | --- |
| `---` | Vanha tiedosto |
| `+++` | Uusi tiedosto |
| `@@ -a,b +c,d @@` | "Hunk"-otsikko: vanhasta tiedostosta rivit a–(a+b-1), uudesta c–(c+d-1) |
| `-` rivin alussa | Rivi oli vanhassa, poistettu |
| `+` rivin alussa | Rivi on uudessa, lisätty |
| (ei merkkiä) | Muuttumaton konteksti-rivi |

## Hakemistojen vertailu

```bash
diff -r kansio1/ kansio2/          # vertaile rekursiivisesti
diff -rq kansio1/ kansio2/           # -q: näytä vain MITKÄ tiedostot eroavat, ei sisältöä
diff -r --brief kansio1/ kansio2/       # sama kuin -q pitkänä muotona
```

## Erojen ohittaminen

```bash
diff -w tiedosto1 tiedosto2     # ohita kaikki välilyönnit/sisennykset
diff -b tiedosto1 tiedosto2       # ohita vain välilyöntien MÄÄRÄN muutokset
diff -B tiedosto1 tiedosto2         # ohita tyhjien rivien lisäykset/poistot
diff -i tiedosto1 tiedosto2           # älä välitä kirjainkoosta
```

## Poistumiskoodit (hyödyllinen skripteissä)

```bash
diff tiedosto1 tiedosto2
echo $?    # 0 = identtiset, 1 = eroavat, 2 = virhe (esim. tiedostoa ei löydy)
```

```bash
if diff -q vanha.conf uusi.conf > /dev/null; then
  echo "Ei muutoksia"
else
  echo "Konfiguraatio on muuttunut"
fi
```

## Patch-tiedoston luonti ja käyttö

```bash
diff -u vanha.txt uusi.txt > muutos.patch
patch vanha.txt < muutos.patch          # sovella patch tiedostoon (muokkaa paikallaan)
patch -p1 < muutos.patch                  # git-tyylinen diff (a/ b/ -etuliitteet) — -p1 pudottaa ensimmäisen polkuosan
```

## macOS-huomio

macOS:n mukana tuleva `diff` on BSD-versio, jolta puuttuu osa GNU
diffin ominaisuuksista (esim. `--color`). Jos GNU-yhteensopivuus on
tarpeen (esim. skriptejä varten, jotka on kirjoitettu Linux-ympäristöä
ajatellen):

```bash
brew install diffutils
```
Tämä asentaa GNU diffin `gdiff`-nimisenä, jotta se ei korvaa
järjestelmän omaa `diff`-komentoa (ks. Homebrew-lunttilappu).

## Katso myös

Versionhallinnassa `git diff` tekee saman asian committien/tilan
välillä sisäänrakennetusti (ks. Git-lunttilappu) — tavallista
`diff`-komentoa tarvitaan lähinnä versionhallinnan ulkopuolisten
tiedostojen vertailuun.
