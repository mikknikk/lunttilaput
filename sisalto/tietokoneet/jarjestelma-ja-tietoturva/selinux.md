---
title: SELinux
---

SELinux (Security-Enhanced Linux) on pakollisen pääsynvalvonnan (MAC)
kerros RHEL-perheen jakeluissa (RHEL, CentOS/Stream, Rocky, AlmaLinux,
Fedora) — rajoittaa prosesseja niiden omiin "konteksteihinsa" riippumatta
tavallisista Unix-oikeuksista (`rwx`).

## Tilan tarkistus

```bash
getenforce                # Enforcing / Permissive / Disabled
sestatus                    # yksityiskohtaisempi tila
setenforce 0                  # vaihda väliaikaisesti Permissive-tilaan (ei estä, vain lokittaa)
setenforce 1                    # takaisin Enforcing-tilaan
```
Pysyvä tilan muutos tehdään `/etc/selinux/config`-tiedostoon
(`SELINUX=enforcing|permissive|disabled`) ja vaatii uudelleenkäynnistyksen.

## Kontekstien tarkastelu

```bash
ls -Z tiedosto           # tiedoston SELinux-konteksti
ps -Z                       # prosessien kontekstit
id -Z                          # oman istunnon konteksti
```
Konteksti on muotoa `käyttäjä:rooli:tyyppi:taso` — käytännön työssä
lähes aina **tyyppi** (`_t`-loppuinen, esim. `httpd_sys_content_t`) on
se, mikä ratkaisee sallitun toiminnan.

## Kontekstin muuttaminen: `chcon` vs. `restorecon`

```bash
chcon -t httpd_sys_content_t tiedosto        # väliaikainen — katoaa relabel-ajossa
chcon -R -t httpd_sys_content_t /srv/web        # rekursiivisesti

restorecon -v tiedosto                             # palauta oletuskontekstiin (policyn mukainen)
restorecon -R -v /srv/web                            # rekursiivisesti
```
`chcon` muuttaa vain kyseisen tiedoston senhetkisen kontekstin — se ei
ole pysyvä, vaan katoaa esim. `restorecon`-ajossa tai koko
tiedostojärjestelmän relabeloinnissa. Pysyvään muutokseen tarvitaan
`semanage fcontext`.

## Pysyvät kontekstisäännöt: `semanage fcontext`

```bash
semanage fcontext -l                                     # listaa nykyiset säännöt
semanage fcontext -a -t httpd_sys_content_t "/srv/web(/.*)?"   # lisää uusi sääntö (regex-polku)
restorecon -R -v /srv/web                                    # sovella lisätty sääntö tiedostoihin
```
`semanage fcontext` tallentaa säännön pysyvästi
(`file_contexts.local`), ja `restorecon` soveltaa sen — nämä kaksi
kulkevat aina yhdessä: sääntö ilman `restorecon`-ajoa ei vaikuta jo
olemassa oleviin tiedostoihin.

## Boolean-asetukset (valmiiksi määritellyt käytäntökytkimet)

```bash
getsebool -a                          # listaa kaikki boolean-asetukset ja niiden tilan
getsebool httpd_can_network_connect     # yhden asetuksen tila
setsebool httpd_can_network_connect on    # aseta väliaikaisesti (nollautuu uudelleenkäynnistyksessä)
setsebool -P httpd_can_network_connect on   # aseta pysyvästi
```

## Porttien salliminen palvelulle

```bash
semanage port -l                                 # listaa nykyiset porttimääritykset
semanage port -a -t http_port_t -p tcp 8080         # salli httpd kuunnella porttia 8080/tcp
semanage port -d -t http_port_t -p tcp 8080           # poista määritys
```
Tämä tarvitaan esim. kun web-palvelin halutaan ajaa oletusportin
80/443 sijaan jollain muulla portilla — pelkkä palomuurisääntö ei riitä,
jos SELinux ei tunne kyseistä porttia palvelun sallituksi kontekstiksi.

## Vianetsintä: miksi jokin estyi?

```bash
sudo grep denied /var/log/audit/audit.log     # etsi estopäätökset lokista
```

Kun syy on selvillä ja haluat sallia täsmälleen sen toiminnon (ei koko
SELinuxin sammuttamista!):

```bash
grep httpd /var/log/audit/audit.log | audit2allow -M oma_saanto
semodule -i oma_saanto.pp
```
`audit2allow` generoi minimaalisen policy-moduulin havaituista
estopäätöksistä, ja `semodule -i` ottaa sen käyttöön. **Älä** käytä
`setenforce 0` -tilaa pysyvänä ratkaisuna tuotannossa — se sammuttaa koko
suojausmekanismin sen sijaan että korjaisi yksittäisen säännön.
