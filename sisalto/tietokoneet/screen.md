---
title: Screen
---

GNU Screen on terminaalimultiplekseri: mahdollistaa useamman
terminaali-istunnon pyörittämisen yhden yhteyden sisällä ja istunnon
jättämisen taustalle pyörimään (esim. palvelimelle SSH-yhteyden
katketessakin).

## Istunnon hallinta

```bash
screen                    # uusi nimetön istunto
screen -S nimi             # uusi nimetty istunto
screen -ls                  # listaa käynnissä olevat istunnot
screen -r                    # palaa ainoaan irrotettuun istuntoon
screen -r nimi                # palaa nimettyyn istuntoon
screen -d -r nimi              # irrota istunto toisesta päätteestä ja liity siihen itse
```

## Näppäinkomennot (oletusetuliite `Ctrl+a`)

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+a d` | Irrota istunto (detach) — jää pyörimään taustalle |
| `Ctrl+a c` | Uusi ikkuna |
| `Ctrl+a n` / `Ctrl+a p` | Seuraava / edellinen ikkuna |
| `Ctrl+a "` | Listaa kaikki ikkunat valittavaksi |
| `Ctrl+a A` | Nimeä nykyinen ikkuna uudelleen |
| `Ctrl+a k` | Tapa nykyinen ikkuna |
| `Ctrl+a S` | Jaa näyttö vaakasuunnassa |
| `Ctrl+a \|` | Jaa näyttö pystysuunnassa |
| `Ctrl+a Tab` | Vaihda jaettujen alueiden välillä |
| `Ctrl+a Esc` | Vieritystila (selaa historiaa nuolilla, `q` tai `Esc` poistuu) |
| `Ctrl+a x` | Lukitse pääte |

## Yleinen työnkulku palvelimella

```bash
ssh palvelin
screen -S tyo
# ajetaan pitkäkestoinen komento...
# Ctrl+a d irrottaa istunnon
exit
# ... yhteys voi katketa, tämä ei vaikuta istuntoon

ssh palvelin
screen -r tyo    # jatketaan siitä mihin jäätiin
```

## Asetustiedosto `~/.screenrc`

```
hardstatus alwayslastline
hardstatus string '%{= kG}%{-}%H %{= kw}| %= %{= kw}%c %{-}'
defscrollback 5000
startup_message off
```
