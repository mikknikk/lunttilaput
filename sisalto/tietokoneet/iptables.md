---
title: iptables
---

iptables on Linuxin perinteinen palomuurityökalu netfilter-kehykselle.

**Ajankohtainen huomio:** iptables on nykyään Netfilter-projektin
virallisesti "legacy"-tilaan asettama — se saa vielä
tietoturvakorjauksia, mutta ei uusia ominaisuuksia. Kaikki merkittävät
Linux-jakelut (RHEL/AlmaLinux/Rocky 9+, Debian 11+, Ubuntu 22.04+,
Fedora 35+, Arch huhtikuusta 2026 alkaen) käyttävät oletuksena
**nftables**-taustamoottoria — `iptables`-komennot toimivat näissä
edelleen samalla syntaksilla, mutta reitittyvät `iptables-nft`
-yhteensopivuuskerroksen kautta oikean nftables-moottorin läpi. Uusiin
järjestelmiin kannattaa harkita suoraan `nft`-komentoa tai
`firewalld`/`ufw`-tason työkalua, mutta alla olevat komennot toimivat
silti käytännössä kaikkialla.

## Perusrakenne

Säännöt on jaettu **ketjuihin** (chains): `INPUT` (saapuva liikenne
tälle koneelle), `OUTPUT` (lähtevä liikenne tältä koneelta), `FORWARD`
(reititettävä liikenne). Oletustaulu on `filter`.

## Sääntöjen listaus

```bash
sudo iptables -L                       # listaa filter-taulun säännöt
sudo iptables -L -v -n                  # yksityiskohtaisemmin, ei DNS-käännöstä
sudo iptables -L INPUT --line-numbers     # rivinumerot poistoa varten
```

## Sääntöjen lisäys

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT     # lisää listan loppuun
sudo iptables -I INPUT 1 -p tcp --dport 443 -j ACCEPT    # lisää tiettyyn kohtaan (tässä ensimmäiseksi)
sudo iptables -A INPUT -s 10.0.0.5 -j DROP                # pudota tietystä IP:stä tuleva liikenne
sudo iptables -A INPUT -i lo -j ACCEPT                     # salli kaikki paikallinen (loopback) liikenne
```

## Sääntöjen poisto

```bash
sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT     # poista täsmäävä sääntö
sudo iptables -D INPUT 3                                  # poista rivinumeron perusteella
sudo iptables -F                                            # tyhjennä kaikki säännöt nykyisestä taulusta
```

## Kohteet (targets)

| Kohde | Kuvaus |
| --- | --- |
| `ACCEPT` | Salli paketti |
| `DROP` | Pudota paketti hiljaisesti (ei vastausta lähettäjälle) |
| `REJECT` | Hylkää paketti ja lähetä virheilmoitus takaisin |
| `LOG` | Kirjaa paketti lokiin ja jatka seuraavaan sääntöön |

## Oletuskäytäntö (default policy)

```bash
sudo iptables -P INPUT DROP      # pudota oletuksena kaikki saapuva
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT
```
**Varoitus:** aseta oletuskäytäntö `DROP`:ksi vasta sen jälkeen, kun olet
lisännyt tarvittavat `ACCEPT`-säännöt (mm. SSH:lle) — muuten voit
lukita itsesi ulos etäpalvelimelta.

## Yleisiä esimerkkejä

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT               # SSH
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT  # olemassa olevat yhteydet
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT      # ping
```

## Sääntöjen pysyvyys

iptables-säännöt eivät oletuksena säily uudelleenkäynnistyksen yli —
ne pitää tallentaa erikseen:

```bash
sudo iptables-save > /etc/iptables/rules.v4
sudo iptables-restore < /etc/iptables/rules.v4
```
Monessa jakelussa tähän on oma paketti (esim. Debian/Ubuntu:
`iptables-persistent`), joka lataa tallennetut säännöt automaattisesti
käynnistyksessä.
