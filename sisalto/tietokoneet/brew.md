---
title: Homebrew
---

Homebrew (komento `brew`) on macOS:n (ja Linuxin) suosituin
pakettienhallintajärjestelmä komentoriville. Apple Siliconilla paketit
asentuvat oletuksena hakemistoon `/opt/homebrew`, Intel-Maceilla
`/usr/local`.

## Perusasennus

```bash
brew install git
brew install --cask visual-studio-code   # graafiset sovellukset (cask)
brew uninstall git
```

## Päivitykset

```bash
brew update            # päivitä Homebrewin oma pakettitietokanta
brew upgrade            # päivitä kaikki asennetut paketit
brew upgrade git         # päivitä vain yksi paketti
brew outdated            # listaa paketit, joille on päivitys saatavilla
```

## Tiedonhaku

```bash
brew search nginx
brew info git
brew list                # kaikki asennetut paketit
brew list --cask          # asennetut graafiset sovellukset
brew deps git             # riippuvuudet
brew uses --installed git # mitkä asennetut paketit riippuvat tästä
```

## Siivous

```bash
brew cleanup              # poista vanhat versiot ja välimuisti
brew cleanup -n            # näytä mitä poistettaisiin (kuivaharjoittelu)
brew autoremove            # poista orvoiksi jääneet riippuvuudet
```

## Vianetsintä

```bash
brew doctor                # tarkista asennuksen kunto ja tyypilliset ongelmat
brew config                # näytä ympäristön tiedot (hyödyllinen bugi-ilmoituksiin)
```

## Palvelut (taustaprosessit)

Monet paketit (esim. tietokannat) asentavat mukana `brew services`
-hallittavan taustapalvelun:

```bash
brew services list
brew services start postgresql@16
brew services stop postgresql@16
brew services restart postgresql@16
```

## Tapit (taps) — lisärepositoriot

```bash
brew tap homebrew/cask-fonts
brew untap homebrew/cask-fonts
```
Tap tuo käyttöön lisää paketteja virallisen ydinrepositorion ulkopuolelta.

## Brewfile — koko asennuksen kuvaus tiedostona

```bash
brew bundle dump              # tallenna nykyiset paketit Brewfile-tiedostoon
brew bundle install            # asenna Brewfile:ssa listatut paketit
brew bundle check              # tarkista puuttuuko jotain asentamatta
```
Hyödyllinen uuden koneen asetuksien toistamiseen tai tiimin yhteisen
työkalupakin ylläpitoon versionhallinnassa.
