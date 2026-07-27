---
title: Oh My Zsh
---

Oh My Zsh on suosittu yhteisövetoinen kehys zsh-asetusten hallintaan:
satoja valinnaisia laajennuksia (plugins), kymmeniä teemoja ja
sisäänrakennettu päivitystyökalu.

## Asennus

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Asennus luo `~/.zshrc`-tiedoston valmiista mallipohjasta, jos sitä ei
vielä ole, ja asettaa `$ZSH`-muuttujan osoittamaan asennuskansioon
(oletuksena `~/.oh-my-zsh`).

## Laajennusten (plugins) käyttöönotto

```zsh
# ~/.zshrc
plugins=(git docker macos pyenv)
```
**Huomio:** zsh-taulukon alkiot erotellaan välilyönnillä, ei
pilkulla — `plugins=(git, docker)` ei toimi odotetusti.

Rivi pitää olla ennen `source $ZSH/oh-my-zsh.sh`-riviä tiedostossa.

## `omz`-komentorivityökalu

```bash
omz update                    # päivitä Oh My Zsh manuaalisesti
omz plugin list                  # listaa käytettävissä olevat laajennukset
omz plugin enable docker          # ota laajennus käyttöön (muokkaa .zshrc:tä puolestasi)
omz plugin disable docker          # poista käytöstä
omz theme list                       # listaa saatavilla olevat teemat
omz reload                             # lataa asetukset uudelleen
```

## Automaattiset päivitykset

Oletuksena Oh My Zsh kysyy päivityksestä n. 2 viikon välein. Tätä voi
säätää `.zshrc`:ssä ennen Oh My Zshin latausriviä:

```zsh
zstyle ':omz:update' mode auto        # päivitä kysymättä
zstyle ':omz:update' frequency 7        # tarkista 7 päivän välein
```

## Suositut kolmannen osapuolen lisäosat

Näitä ei ole mukana oletuksena, vaan ne asennetaan erikseen
`$ZSH_CUSTOM/plugins/`-kansioon (oletuksena
`~/.oh-my-zsh/custom/plugins/`):

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
Lisää sen jälkeen `plugins`-listaan: `plugins=(git zsh-autosuggestions
zsh-syntax-highlighting)`. `zsh-syntax-highlighting` kannattaa laittaa
listan viimeiseksi, koska se tarvitsee muiden laajennusten olevan jo
ladattuna.

## Teeman vaihto

```zsh
# ~/.zshrc
ZSH_THEME="robbyrussell"    # oletusteema
```
Kolmannen osapuolen teemat (esim. Powerlevel10k) asennetaan samaan
tapaan kuin kolmannen osapuolen laajennuksetkin, `$ZSH_CUSTOM/themes/`
-kansioon.
