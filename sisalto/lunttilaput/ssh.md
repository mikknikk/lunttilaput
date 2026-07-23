---
title: SSH:n lunttilappu
---

## Peruskäyttö

```bash
ssh kayttaja@palvelin
ssh -p 2222 kayttaja@palvelin    # muu kuin oletusportti
ssh -i ~/.ssh/oma_avain kayttaja@palvelin
```

## Avainparin luonti

```bash
ssh-keygen -t ed25519 -C "kommentti"
ssh-copy-id kayttaja@palvelin   # vie julkinen avain palvelimelle
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

## Tiedostojen siirto

```bash
scp tiedosto.txt kayttaja@palvelin:/polku/
rsync -avz kansio/ kayttaja@palvelin:/polku/kansio/
```

## Tunnelointi

```bash
ssh -L 8080:localhost:80 kayttaja@palvelin   # paikallinen portti etäpalveluun
ssh -D 1080 kayttaja@palvelin                # SOCKS-proxy
```

## Vianetsintä

```bash
ssh -v kayttaja@palvelin        # tulostaa yhteyden muodostuksen vaiheittain
ssh-keyscan -H palvelin         # hae palvelimen host key tunnetuksi
```
