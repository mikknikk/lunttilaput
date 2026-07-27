---
title: tmux
---

tmux on GNU Screeniä uudempi terminaalimultiplekseri: istunnot,
ikkunat ja jaetut paneelit (panes) yhden yhteyden sisällä, istunto jää
elämään myös yhteyden katketessa.

## Istunnon hallinta

```bash
tmux                      # uusi nimetön istunto
tmux new -s nimi            # uusi nimetty istunto
tmux ls                       # listaa istunnot
tmux attach -t nimi             # liity nimettyyn istuntoon
tmux kill-session -t nimi        # tapa istunto
```

## Näppäinkomennot (oletusetuliite `Ctrl+b`)

| Näppäin | Kuvaus |
| --- | --- |
| `Ctrl+b d` | Irrota istunto (detach) |
| `Ctrl+b c` | Uusi ikkuna |
| `Ctrl+b n` / `Ctrl+b p` | Seuraava / edellinen ikkuna |
| `Ctrl+b <numero>` | Hyppää tiettyyn ikkunaan |
| `Ctrl+b ,` | Nimeä ikkuna uudelleen |
| `Ctrl+b w` | Listaa ikkunat valittavaksi |
| `Ctrl+b %` | Jaa paneeli pystysuunnassa |
| `Ctrl+b "` | Jaa paneeli vaakasuunnassa |
| `Ctrl+b <nuoli>` | Siirry paneelien välillä |
| `Ctrl+b z` | Suurenna/palauta nykyinen paneeli |
| `Ctrl+b x` | Sulje nykyinen paneeli |
| `Ctrl+b [` | Vieritystila/kopiointitila (`q` poistuu) |

## Paneelien koon muutos

```
Ctrl+b Ctrl+<nuoli>    " muuta paneelin kokoa askel kerrallaan
```

## Asetustiedosto `~/.tmux.conf`

```
set -g mouse on                     # hiiren käyttö paneelien/koon valintaan
set -g history-limit 10000
set -g prefix C-a                    # vaihda etuliite Ctrl+b:stä Ctrl+a:han
unbind C-b
bind C-a send-prefix
```
Muutosten jälkeen lataa asetukset uudelleen istunnon sisältä:
```
Ctrl+b :
source-file ~/.tmux.conf
```

## Skriptaus ja automaatio

```bash
tmux new-session -d -s tyo          # luo istunto taustalle ilman liittymistä
tmux send-keys -t tyo 'komento' Enter  # lähetä komento istuntoon
tmux attach -t tyo
```
Tätä käytetään usein käynnistysskripteissä, jotka pystyttävät valmiin
ikkuna-/paneelilayoutin automaattisesti.
