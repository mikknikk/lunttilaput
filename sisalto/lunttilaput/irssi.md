---
title: Irssin lunttilappu
---

## Yhdistäminen

```
/connect irc.esimerkki.fi
/server add -auto -network Esimerkki irc.esimerkki.fi 6697
/network add -sasl_mechanism PLAIN -sasl_username nimi -sasl_password salasana Esimerkki
```

## Kanavat

| Komento | Kuvaus |
| --- | --- |
| `/join #kanava` | Liity kanavalle |
| `/part #kanava` | Poistu kanavalta |
| `/window close` | Sulje nykyinen ikkuna |
| `/names` | Listaa kanavan käyttäjät |

## Ikkunoiden hallinta

| Komento | Kuvaus |
| --- | --- |
| `Ctrl+N` / `Ctrl+P` | Seuraava / edellinen ikkuna |
| `Alt+<numero>` | Hyppää suoraan ikkunaan |
| `/window move <numero>` | Siirrä ikkuna toiseen paikkaan |

## Yksityisviestit ja huomiot

```
/query nimimerkki
/msg nimimerkki viesti
/notify nimimerkki
```

## Lokit

```
/set autolog on
/set autolog_path ~/irclogs/$tag/$0.log
```
