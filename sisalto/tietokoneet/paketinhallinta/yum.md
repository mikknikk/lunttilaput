---
title: Yum
---

Yum (Yellowdog Updater, Modified) on RPM-pohjaisten Linux-jakelujen
(RHEL, CentOS, Fedora, Rocky Linux, AlmaLinux) perinteinen
pakettienhallintakomento.

**Tärkeä huomio nykytilasta:** RHEL 8:sta ja CentOS 8:sta alkaen
taustalla toimiva moottori on korvattu DNF:llä (Dandified YUM) —
`yum`-komento on nykyisin symbolinen linkki `dnf`:ään. Komennot ja
syntaksi toimivat entiseen tapaan, mutta uusissa asennuksissa kannattaa
harkita `dnf`-komennon käyttöä suoraan, koska se on ainoa aktiivisesti
kehitetty toteutus.

## Pakettien asennus ja poisto

```bash
sudo yum install nginx
sudo yum remove nginx
sudo yum reinstall nginx
```

## Päivitykset

```bash
sudo yum update              # päivitä kaikki paketit
sudo yum update nginx         # päivitä yksi paketti
sudo yum check-update          # listaa saatavilla olevat päivitykset asentamatta
```

## Tiedonhaku

```bash
yum search nginx
yum info nginx
yum list installed
yum list available
yum provides */nginx           # mikä paketti tarjoaa tietyn tiedoston/komennon
```

## Riippuvuudet ja historia

```bash
yum deplist nginx
yum history                     # listaa aiemmat yum-transaktiot
yum history undo <numero>        # peru tietty transaktio
```

## Repositoriot

```bash
yum repolist                    # listaa käytössä olevat repositoriot
yum repolist all                 # myös poistetut käytöstä
sudo yum-config-manager --add-repo <url>
```

## Siivous

```bash
sudo yum clean all               # tyhjennä välimuistit (metatiedot, paketit)
sudo yum autoremove                # poista orvoiksi jääneet riippuvuudet
```

## Ryhmät (group)

```bash
yum group list                   # listaa pakettiryhmät (esim. "Development Tools")
sudo yum group install "Development Tools"
```
