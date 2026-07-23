---
title: SSH
---

## Peruskäyttö

```bash
ssh kayttaja@palvelin
ssh -p 2222 kayttaja@palvelin    # muu kuin oletusportti
ssh -i ~/.ssh/oma_avain kayttaja@palvelin
ssh kayttaja@palvelin "komento etäpalvelimella"   # aja yksi komento ja poistu
```

## Avainparin luonti

```bash
ssh-keygen -t ed25519 -C "kommentti"
ssh-keygen -t ed25519 -f ~/.ssh/erillinen_avain -N ""   # ei salasanaa, esim. CI:tä varten
ssh-copy-id kayttaja@palvelin   # vie julkinen avain palvelimelle
ssh-add ~/.ssh/oma_avain         # lisää avain käynnissä olevaan ssh-agenttiin
ssh-add -l                       # listaa agentin avaimet
```

## `~/.ssh/config` — pikakutsut

```
Host lyhytnimi
  HostName palvelin.esimerkki.fi
  User kayttaja
  Port 22
  IdentityFile ~/.ssh/oma_avain
```
Tämän jälkeen riittää `ssh lyhytnimi`.

## Hyppypalvelimen (jump host) kautta yhdistäminen

```
Host sisaverkko
  HostName 10.0.0.5
  User kayttaja
  ProxyJump hyppypalvelin
```
tai suoraan komentoriviltä: `ssh -J hyppypalvelin kayttaja@10.0.0.5`.

## Yhteyden kierrätys (multiplexing)

Nopeuttaa perättäisiä yhteyksiä samaan palvelimeen käyttämällä yhtä
taustayhteyttä uudelleen:

```
Host *
  ControlMaster auto
  ControlPath ~/.ssh/sockets/%r@%h-%p
  ControlPersist 10m
```

## Tiedostojen siirto

```bash
scp tiedosto.txt kayttaja@palvelin:/polku/
scp -r kansio/ kayttaja@palvelin:/polku/            # koko kansio
rsync -avz kansio/ kayttaja@palvelin:/polku/kansio/
sshfs kayttaja@palvelin:/polku/ ~/paikallinen/liitos/   # liitä etähakemisto tiedostojärjestelmään
```

## Tunnelointi

```bash
ssh -L 8080:localhost:80 kayttaja@palvelin   # paikallinen portti etäpalveluun
ssh -R 9000:localhost:3000 kayttaja@palvelin  # etäpalvelimen portti paikalliseen palveluun
ssh -D 1080 kayttaja@palvelin                # SOCKS-proxy
ssh -N -L 8080:localhost:80 kayttaja@palvelin  # tunneli ilman komentotulkkia
```

## X11-forwarding

```bash
ssh -X kayttaja@palvelin    # graafisten sovellusten ikkunat omalle koneelle
ssh -Y kayttaja@palvelin    # "luotettu" X11-forwarding (vähemmän rajoituksia)
```

## Agentin välitys (agent forwarding)

```bash
ssh -A kayttaja@palvelin
```
Sallii etäpalvelimen käyttää paikallista ssh-agenttiasi (esim. git-pushiin
toiselle palvelimelle sieltä käsin) ilman että yksityinen avain kopioidaan
sinne. Käytä vain luotettuihin palvelimiin, koska palvelimen root voi
väärinkäyttää agenttiasi sen ollessa auki.

## Vianetsintä

```bash
ssh -v kayttaja@palvelin        # tulostaa yhteyden muodostuksen vaiheittain (-vv, -vvv lisää)
ssh-keyscan -H palvelin         # hae palvelimen host key tunnetuksi
ssh-keygen -R palvelin          # poista vanhentunut host key known_hosts-tiedostosta
```
