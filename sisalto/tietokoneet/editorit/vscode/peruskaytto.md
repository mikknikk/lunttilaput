---
title: Peruskäyttö
---

## Komentopaletti ja pikanäppäimet

| Näppäin (Mac) | Näppäin (Win/Linux) | Kuvaus |
| --- | --- | --- |
| `Cmd+Shift+P` | `Ctrl+Shift+P` | Komentopaletti |
| `Cmd+P` | `Ctrl+P` | Pikatiedostohaku |
| `Cmd+Shift+F` | `Ctrl+Shift+F` | Haku koko projektista |
| `Cmd+B` | `Ctrl+B` | Näytä/piilota sivupalkki |
| `Cmd+J` | `Ctrl+J` | Näytä/piilota terminaali |
| `` Ctrl+` `` | `` Ctrl+` `` | Uusi/aktiivinen integroitu terminaali |
| `Cmd+,` | `Ctrl+,` | Asetukset |

## Muokkaus

| Näppäin (Mac) | Näppäin (Win/Linux) | Kuvaus |
| --- | --- | --- |
| `Cmd+D` | `Ctrl+D` | Valitse seuraava sama sana (moninkertainen kursori) |
| `Cmd+/` | `Ctrl+/` | Kommentoi/poista kommentti rivi |
| `Option+Up/Down` | `Alt+Up/Down` | Siirrä rivi ylös/alas |
| `Shift+Option+Down` | `Shift+Alt+Down` | Kopioi rivi alas |
| `Cmd+Shift+K` | `Ctrl+Shift+K` | Poista rivi |
| `F2` | `F2` | Nimeä symboli uudelleen (koko projektissa) |
| `Cmd+.` | `Ctrl+.` | Näytä pikakorjaukset (quick fix) |

## Navigointi koodissa

| Näppäin (Mac) | Näppäin (Win/Linux) | Kuvaus |
| --- | --- | --- |
| `F12` | `F12` | Siirry määrittelyyn |
| `Option+F12` | `Alt+F12` | Näytä määrittely (peek) |
| `Shift+F12` | `Shift+F12` | Näytä kaikki viittaukset |
| `Cmd+Click` | `Ctrl+Click` | Siirry määrittelyyn hiirellä |
| `Ctrl+-` | `Ctrl+-` | Palaa edelliseen sijaintiin (sama näppäin molemmilla alustoilla) |

## Asetustiedostot työtilassa

```
.vscode/
  settings.json     # projektikohtaiset asetukset
  extensions.json    # suositellut laajennukset
  launch.json        # debuggerin käynnistysasetukset
  tasks.json          # määritellyt tehtävät (build, test...)
```

## `settings.json`-esimerkki

```json
{
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "files.trimTrailingWhitespace": true
}
```

## Integroitu Git

- Lähdehallinta-välilehti (`Cmd+Shift+G` / `Ctrl+Shift+G`) näyttää muutokset,
  mahdollistaa stagen/committin ilman komentoriviä.
- Rivien vieressä näkyvät muutosindikaattorit (lisätty/muokattu/poistettu).
- Sisäänrakennettu diff-näkymä tiedoston historiaa selattaessa.

## Debuggaus

- `F5` käynnistää debuggauksen `launch.json`:n mukaisella konfiguraatiolla.
- `F9` asettaa/poistaa breakpointin nykyiselle riville.
- `F10` / `F11` astuu seuraavaan riviin / sisään funktioon debugatessa.

## Laajennukset komentoriviltä

```bash
code --install-extension julkaisija.laajennus
code --list-extensions
code .              # avaa nykyinen kansio VS Codessa
```
