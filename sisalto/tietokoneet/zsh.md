---
title: Zsh
---

Zsh (Z shell) on bashia laajemmilla ominaisuuksilla varustettu komentotulkki
— macOS:n oletuskomentotulkki Catalinasta (10.15) lähtien.

## Asetustiedostot

| Tiedosto | Ladataan |
| --- | --- |
| `~/.zshenv` | Aina, myös ei-interaktiivisissa/skripteissä |
| `~/.zprofile` | Kirjautumisistunnoissa, ennen `.zshrc`:tä |
| `~/.zshrc` | Interaktiivisissa istunnoissa — tähän useimmat asetukset |
| `~/.zlogin` | Kirjautumisistuntojen jälkeen |

## Hyödyllisiä `setopt`-asetuksia

```zsh
setopt AUTO_CD                 # kirjoita pelkkä kansion nimi cd:n sijaan
setopt CORRECT                  # ehdota korjausta kirjoitusvirheeseen
setopt HIST_IGNORE_DUPS          # älä tallenna peräkkäisiä duplikaattikomentoja
setopt SHARE_HISTORY               # jaa historia avoimien istuntojen kesken reaaliaikaisesti
setopt EXTENDED_GLOB                 # laajennettu globbing (katso alla)
```

## Laajennettu globbing (tiedostohaut)

```zsh
ls *.txt~backup.txt      # kaikki .txt paitsi backup.txt (EXTENDED_GLOB)
ls **/*.py                # kaikki .py-tiedostot rekursiivisesti alikansioista
ls *(.)                     # vain tiedostot, ei kansioita
ls *(/)                      # vain kansiot
ls *(.om[1])                  # uusin muokattu tiedosto
```

## Täydennysjärjestelmä (completion)

```zsh
autoload -Uz compinit
compinit
```
Otetaan käyttöön `.zshrc`:ssä — mahdollistaa mm. `cd <Tab>`,
`git checkout <Tab>` ja komentokohtaiset älykkäät täydennykset.

## Historia

```zsh
history                   # näytä komentohistoria
!!                          # toista edellinen komento
!42                          # toista historian rivi 42
Ctrl+R                        # hae historiasta interaktiivisesti
```

## Prompt ja teemat

Zsh tukee `PROMPT`/`PS1`-muuttujan lisäksi teemajärjestelmiä (esim.
`prompt` sisäänrakennettu teema-apuri, tai Oh My Zsh / Powerlevel10k
-tyyppiset kolmannen osapuolen kehykset — ks. Oh My Zsh -lunttilappu).

## Alias- ja funktioesimerkkejä

```zsh
alias ll='ls -la'
alias gs='git status'

mkcd() {
  mkdir -p "$1" && cd "$1"
}
```

## Zsh vs. bash — keskeisimmät erot

- Globbing on oletuksena tiukempi: täsmäämätön kuvio (`ls *.foo` kun
  yhtään `.foo`-tiedostoa ei ole) aiheuttaa virheen bashista poiketen,
  ellei `setopt NULL_GLOB` ole käytössä.
- Taulukoiden indeksointi alkaa 1:stä, ei 0:sta.
- Sanahaku (`$var[2,4]`) ja monet muut merkkijono-/taulukko-operaatiot
  poikkeavat syntaksiltaan bashista.
