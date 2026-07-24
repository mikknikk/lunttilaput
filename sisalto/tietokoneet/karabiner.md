---
title: Karabiner-Elements
---

Karabiner-Elements on macOS:n näppäimistön uudelleenmäärittelytyökalu:
yksinkertaiset näppäinvaihdot GUI:sta sekä monimutkaiset,
JSON-pohjaiset "Complex Modifications" -säännöt.

## Asetustiedoston sijainti

```
~/.config/karabiner/karabiner.json
```
Karabiner-Elements tarkkailee tätä tiedostoa ja lataa muutokset
automaattisesti. **Huomio:** tarkkailu perustuu yläkansion
(`~/.config/karabiner/`) tapahtumiin — jos korvaat koko yläkansion
(esim. palauttamalla varmuuskopiosta), muutosta ei välttämättä
havaita ilman sovelluksen uudelleenkäynnistystä.

Jos haluat synkronoida asetukset versionhallinnassa/toisten koneiden
kesken, tee symlinkki **koko `~/.config/karabiner`-kansiolle**, ei
pelkälle `karabiner.json`-tiedostolle — muuten muutosten tarkkailu ei
toimi.

## Valmiiden sääntöjen tuonti

```
~/.config/karabiner/assets/complex_modifications/
```
Lataa `.json`-sääntötiedosto (esim.
[ke-complex-modifications.pqrs.org](https://ke-complex-modifications.pqrs.org/))
tähän kansioon, ja se ilmestyy valittavaksi:

```
Karabiner-Elements → Settings → Complex Modifications → Add predefined rule
```

## Virheenetsintä

```
~/.local/share/karabiner/log/console_user_server.log
```
JSON-jäsennysvirheet näkyvät tässä lokissa.

Varmuuskopiot: `~/.config/karabiner/automatic_backups/karabiner_YYYYMMDD.json`.

## Complex modification -säännön perusrakenne

```json
{
  "title": "Omat säännöt",
  "rules": [
    {
      "description": "Caps Lock -> Control (pidettynä) / Escape (napautettuna)",
      "manipulators": [
        {
          "type": "basic",
          "from": { "key_code": "caps_lock" },
          "to": [{ "key_code": "left_control" }],
          "to_if_alone": [{ "key_code": "escape" }]
        }
      ]
    }
  ]
}
```
Tämä on erittäin yleinen ensimmäinen sääntö: Caps Lock toimii
Controlina kun sitä pidetään pohjassa yhdessä toisen näppäimen kanssa,
mutta lähettää Escapen jos se napautetaan yksinään.

## JSON-kommentit

Karabinerin oma konfiguraatiotiedosto sallii `//`- ja `/* */`-kommentit,
mutta **ne katoavat**, jos muokkaat asetuksia GUI:n kautta sen jälkeen —
käsin kirjoitetut kommentit kannattaa siis säilyttää erillisessä
versionhallinnassa olevassa kopiossa.

## Profiilit

Karabiner tukee useampaa profiilia (esim. eri asetukset eri
näppäimistöille) — profiilien välillä vaihdetaan valikosta tai
`karabiner.json`:n `"profiles"`-taulukon `"selected"`-kentän kautta.
