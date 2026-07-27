---
title: Podman
---

Podman on daemoniton konttityökalu — toisin kuin Docker, se ei tarvitse
taustalla pyörivää root-oikeuksin ajettavaa palvelinprosessia. Komentorivi
on suurelta osin yhteensopiva Docker CLI:n kanssa, joten moni `docker
...`-komento toimii sellaisenaan korvaamalla `docker` sanalla `podman`.

## Peruskomennot

```bash
podman pull nginx:alpine
podman run -d --name web -p 8080:80 nginx:alpine
podman ps                    # käynnissä olevat kontit
podman ps -a                 # myös pysäytetyt
podman logs web
podman exec -it web sh
podman stop web
podman rm web
```

## Kuvien hallinta

```bash
podman images
podman rmi nginx:alpine
podman image prune           # poista käyttämättömät, roikkuvat kuvat
podman image prune -a        # poista kaikki käyttämättömät kuvat
podman build -t oma-sovellus .
```

## Podit — konttien ryhmittely

Pod on joukko kontteja, jotka jakavat verkko- ja IPC-nimiavaruuden ja
tavoittavat toisensa `localhost`:n kautta. Sama käsite kuin Kubernetesin
pod — siksi Podmanilla voi tuottaa ja kuluttaa Kubernetes-YAML:ia.

```bash
podman pod create --name oma-pod -p 8080:80
podman run -d --pod oma-pod --name web nginx:alpine
podman run -d --pod oma-pod --name db postgres:16
podman pod list
podman pod stop oma-pod
podman pod rm -f oma-pod
```

## Kubernetes-YAML

```bash
podman generate kube web > web-pod.yaml     # kontista
podman generate kube oma-pod > pod.yaml     # podista
podman play kube pod.yaml                   # aja YAML:sta
podman play kube --down pod.yaml            # pysäytä ja poista
```

## Rootless-turvallisuusmalli

Podman ajaa koko konttipinon tavallisena käyttäjänä — kontin sisäinen
root (UID 0) kuvataan `/etc/subuid`-alueelta löytyvään oikeudettomaan
UID:iin isäntäkoneella. Ei root-omisteista taustaprosessia eikä
setuid-polkua, joten kontista karkaaminen päätyy oikeudettomaksi
"nobody"-käyttäjäksi isännällä root-oikeuksien sijaan.

## Podman Machine (macOS/Windows)

Kontit vaativat Linux-ytimen, joten macOS/Windows-koneella Podman ajaa
kevyttä Linux-VM:ää taustalla:

```bash
podman machine init --cpus 4 --disk-size 50 --memory 4096
podman machine start
podman machine list
podman machine stop
podman machine rm            # nollaa VM, jos se korruptoituu
```

VM on oletuksena rootless-tilassa. Jos kontti tarvitsee root-oikeuksia
(esim. portti < 1024) tai yhteensopivuusongelmia ilmenee:

```bash
podman machine set --rootful
```

## Docker Compose -yhteensopivuus

Podman ei paljasta Docker-yhteensopivaa APIa macOS:ssä oletuksena.
Yksinkertaisin tapa käyttää olemassa olevia `docker-compose.yml`
-tiedostoja on Podmanin sisäänrakennettu compose-komento:

```bash
podman compose up -d
```

Vaihtoehtoisesti virallinen Docker Compose -CLI saadaan puhumaan Podmanin
kanssa asettamalla `DOCKER_HOST` osoittamaan Podman-koneen socketiin:

```bash
export DOCKER_HOST=unix://$(podman machine inspect --format '{{.ConnectionInfo.PodmanSocket.Path}}')
docker compose up -d
```

## Systemd-integraatio: Quadlet

Podmanilla ei ole daemonia käynnistämässä kontteja uudelleen käynnistyksen
tai kaatumisen jälkeen — tämä hoidetaan systemdillä. Quadlet on nykyaikainen
tapa määritellä kontti deklaratiivisena yksikkötiedostona:

```
~/.config/containers/systemd/web.container    # rootless
/etc/containers/systemd/web.container         # rootful
```

Tiedoston muokkauksen jälkeen:

```bash
systemctl --user daemon-reload      # rootless
sudo systemctl daemon-reload        # rootful

systemctl --user start web.service
systemctl --user enable web.service
```

Rootless-palvelujen pitää pysyä käynnissä myös ilman kirjautunutta
istuntoa (esim. palvelimella):

```bash
sudo loginctl enable-linger $UID
```

## Automaattiset kuvapäivitykset

```bash
systemctl --user enable --now podman-auto-update.timer
```
