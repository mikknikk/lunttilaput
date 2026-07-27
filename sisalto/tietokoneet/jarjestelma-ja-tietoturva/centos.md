---
title: CentOS
---

## Tärkeä ajankohtainen huomio

**Perinteinen CentOS Linux (RHEL:n ilmainen, vakaa uudelleenkäännös) on
kokonaisuudessaan elinkaarensa päässä:**

| Versio | Tuki päättyi |
| --- | --- |
| CentOS Linux 6 ja vanhemmat | 2020 tai aiemmin |
| CentOS Linux 8 | 31.12.2021 |
| CentOS Linux 7 | 30.6.2024 |

Yhtään CentOS Linux -versiota ei pidä enää asentaa uuteen tuotantoon —
tietoturvapäivityksiä ei tule. Tästä huolimatta CentOS 7:ää käytetään
edelleen laajasti tuotannossa migraation työläyden vuoksi — jos ylläpidät
tällaista järjestelmää, migraatio on syytä aikatauluttaa pikaisesti.

## Mihin siirtyä

- **Rocky Linux** — RHEL:n kanssa "bug-for-bug"-yhteensopiva
  uudelleenkäännös, perustettu CentOS-projektin yhden perustajan
  toimesta nimenomaan jatkamaan CentOS Linuxin roolia.
- **AlmaLinux** — vastaava ilmainen, ei-kaupallisin rajoituksin toimiva
  RHEL-yhteensopiva jakelu.
- **CentOS Stream** — CentOS-projektin oma jatko, mutta **ei ole suora
  korvaaja vakaalle CentOS Linuxille**: se on RHEL:n tuleva versio
  "esikatseluna" (rolling release RHEL:n edellä), tarkoitettu ennemmin
  kehittäjille kuin tuotantovakauteen. Red Hat itse ei suosittele sitä
  suoraksi CentOS Linux -korvaajaksi tuotantokäyttöön.
- **RHEL itse** — Red Hatilla on ilmainen kehittäjätilaus pienelle
  määrälle järjestelmiä, jos täysi yritystuki ei ole tarpeen.

Migraatiotyökalu `migrate2rocky` (Rocky Linuxille) tai vastaava
AlmaLinuxille automatisoi siirtymän paikoillaan ilman uudelleenasennusta
useimmissa tapauksissa.

## CentOS/RHEL-perheen yhteiset perustyökalut

Nämä pätevät sekä vanhaan CentOS Linuxiin että sen seuraajiin
(Rocky/AlmaLinux/CentOS Stream), koska ne ovat kaikki samaa RPM-pohjaista
perhettä:

```bash
cat /etc/os-release          # tarkista tarkka jakelu ja versio
rpm -qa                        # listaa kaikki asennetut RPM-paketit
sudo dnf install nginx         # pakettienhallinta (ks. myös Yum-lunttilappu)
sudo systemctl status nginx    # palvelun tila (systemd)
sudo firewall-cmd --list-all   # firewalld-säännöt
getenforce                     # SELinuxin tila (Enforcing/Permissive/Disabled)
```

## SELinux-perusteet

```bash
getenforce                        # nykyinen tila
sudo setenforce 0                  # aseta väliaikaisesti Permissive-tilaan
sudo setenforce 1                  # takaisin Enforcing-tilaan
sestatus                           # tarkempi tilatieto
sudo semanage port -l | grep http  # mitkä portit on sallittu tietylle kontekstille
```
SELinuxin poistaminen kokonaan käytöstä tuotannossa ei ole suositeltavaa
— se on merkittävä osa RHEL-perheen tietoturvamallia.

## firewalld-perusteet

```bash
sudo firewall-cmd --list-all
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload
```

## Yhteenveto

"CentOS" tänä päivänä tarkoittaa käytännössä useampaa eri asiaa: EOL:ttunutta
vanhaa CentOS Linuxia, aktiivisesti kehitettävää mutta tuotantoon
sopimatonta CentOS Streamia, sekä näiden ekosysteemin RHEL-yhteensopivia
seuraajia. Uutta järjestelmää perustettaessa valinta on käytännössä Rocky
Linux, AlmaLinux tai RHEL — ei enää "CentOS" sanan perinteisessä
merkityksessä.
