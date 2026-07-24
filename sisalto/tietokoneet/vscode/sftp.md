---
title: SFTP
---

Tämä lunttilappu koskee `Natizyskunk.sftp`-laajennusta — ylläpidetty
jatkokehitys (fork) alkuperäisestä liximomon SFTP-laajennuksesta, joka on
merkitty markkinapaikalla vanhentuneeksi (deprecated) ja jonka ylläpitäjä
itse suosittelee siirtymään tähän forkkiin.

## Asennus

```
ext install Natizyskunk.sftp
```
tai VS Coden laajennusvälilehdeltä haulla "sftp" (tekijä: Natizyskunk).

## Määrittely: `.vscode/sftp.json`

Luo pohjatiedosto komennolla **SFTP: Config** (komentopaletti
`Cmd+Shift+P` / `Ctrl+Shift+P`). Yksinkertainen esimerkki:

```json
{
  "name": "Tuotanto",
  "host": "palvelin.esimerkki.fi",
  "protocol": "sftp",
  "port": 22,
  "username": "kayttaja",
  "privateKeyPath": "/Users/kayttaja/.ssh/id_ed25519",
  "remotePath": "/var/www/sivusto",
  "uploadOnSave": false,
  "ignore": [
    ".vscode",
    ".git",
    "node_modules"
  ]
}
```

## Useampi ympäristö (profiilit) samassa tiedostossa

```json
{
  "context": ".",
  "protocol": "sftp",
  "host": "palvelin.esimerkki.fi",
  "username": "kayttaja",
  "remotePath": "/var/www/sivusto",
  "profiles": {
    "dev": {
      "host": "dev.esimerkki.fi",
      "remotePath": "/var/www/dev"
    },
    "prod": {
      "host": "palvelin.esimerkki.fi",
      "remotePath": "/var/www/tuotanto"
    }
  }
}
```
Vaihda aktiivinen profiili komennolla **SFTP: Set Profile**.
`context` (paikallinen juurikansio) ja `watcher` toimivat vain
tiedoston juuritasolla, ei yksittäisen profiilin sisällä.

## Komentopaletin komennot

| Komento | Kuvaus |
| --- | --- |
| SFTP: Config | Luo uuden määrittelytiedoston projektille |
| SFTP: Set Profile | Vaihda aktiivinen profiili |
| SFTP: Upload Active File | Vie auki olevan tiedoston palvelimelle |
| SFTP: Download Active File | Nouda tiedoston etäversio, ylikirjoita paikallinen |
| SFTP: Upload Active Folder | Vie koko kansion (jossa auki oleva tiedosto sijaitsee) |
| SFTP: Download Active Folder | Nouda koko kansio etäpalvelimelta |
| SFTP: Upload Changed Files | Vie kaikki committien jälkeen muuttuneet/uudet tiedostot |
| SFTP: Sync Local -> Remote | Synkronoi paikallinen → etä (vain uudemmat/uudet) |
| SFTP: Sync Remote -> Local | Synkronoi etä → paikallinen |
| SFTP: Sync Both Directions | Vertaa muokkausaikoja ja synkronoi tuorein versio kumpaankin suuntaan |
| SFTP: List Active Folder | Listaa auki olevan tiedoston kansion sisällön etäpalvelimella |
| SFTP: Cancel All Transfers | Peruuta kaikki käynnissä olevat siirrot |
| SFTP: Open SSH in Terminal | Avaa terminaali ja kirjaudu automaattisesti palvelimelle |

## Kontekstivalikko (hiiren oikea painike Explorerissa)

| Toiminto | Kuvaus |
| --- | --- |
| Upload | Vie valitut tiedostot/kansiot palvelimelle |
| Download | Nouda valitut tiedostot/kansiot palvelimelta |
| Force Upload | Vie ohittaen `ignore`-säännöt |
| Force Download | Nouda ohittaen `ignore`-säännöt |

## Automaattinen lähetys tallennuksen yhteydessä

```json
{
  "uploadOnSave": true,
  "watcher": {
    "files": "**/*.{php,js,css}",
    "autoUpload": true,
    "autoDelete": false
  }
}
```

## Huomioita

- `.vscode/sftp.json` sisältää usein salasanan tai polun yksityiseen
  avaimeen — lisää se `.gitignore`-tiedostoon, ettei se päädy
  versionhallintaan.
- `privateKeyPath` on suositeltavampi kuin `password`, samasta syystä
  kuin muuallakin SSH-avainten kanssa (ks. SSH-lunttilappu).
