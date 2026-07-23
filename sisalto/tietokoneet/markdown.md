---
title: Markdown
---

## Otsikot

```
# Otsikko 1
## Otsikko 2
### Otsikko 3
```

## Tekstin muotoilu

| Merkintä | Tulos |
| --- | --- |
| `*kursiivi*` tai `_kursiivi_` | *kursiivi* |
| `**lihavointi**` | **lihavointi** |
| `***lihava kursiivi***` | ***lihava kursiivi*** |
| `~~yliviivaus~~` | yliviivaus (jos tuettu) |
| `` `koodi` `` | `koodi` |

## Listat

```
- Kohta 1
- Kohta 2
  - Alakohta
    - Ala-alakohta

1. Ensimmäinen
2. Toinen
   1. Alakohta numeroituna
```

## Tehtävälistat (jos tuettu)

```
- [x] Valmis tehtävä
- [ ] Kesken oleva tehtävä
```

## Linkit ja kuvat

```
[Linkin teksti](https://esimerkki.fi)
[Linkin teksti](https://esimerkki.fi "Työkaluvihje")
![Kuvan vaihtoehtoinen teksti](kuva.png)

[Viitelinkki][1]

[1]: https://esimerkki.fi
```

## Lainaukset

```
> Tämä on lainaus.
> Se voi jatkua usealle riville.
>
> > Sisäkkäinen lainaus.
```

## Koodilohkot

Kolmen backtickin väliin, valinnaisella kielimerkinnällä (mahdollistaa
syntaksikorostuksen):

````
```python
print("Hei maailma")
```
````

Yhden rivin koodi kirjoitetaan yksittäisillä backtickeillä: `` `koodi` ``.

## Taulukot

```
| Sarake 1 | Sarake 2 |
| --- | --- |
| Arvo A | Arvo B |
```

Tasaus voidaan määrittää kaksoispisteillä:

```
| Vasen | Keskitetty | Oikea |
| :--- | :---: | ---: |
| a | b | c |
```

## Vaakaviiva

```
---
```

## Rivinvaihdot

Yksi rivinvaihto lähdekoodissa EI luo uutta riviä tulosteeseen — Markdown
yhdistää perättäiset rivit samaksi kappaleeksi. Pakota rivinvaihto joko
tyhjällä rivillä (uusi kappale) tai lisäämällä kaksi välilyöntiä rivin
loppuun.

## Erikoismerkkien pakotus (escape)

Jos haluat kirjoittaa merkin, joka muuten tulkittaisiin muotoiluna, edeltä se
kenoviivalla: `\*ei kursiivia\*` tulostuu kirjaimellisesti `*ei kursiivia*`.

## Vinkki tälle sivustolle

Jokaisen `.md`-tiedoston alussa voi olla front matter, joka määrittää sivun
otsikon:

```
---
title: Sivun otsikko
---
```

Tämä sivusto tukee taulukoita ja koodilohkoja (`tables`- ja
`fenced_code`-laajennukset), mutta ei esim. tehtävälistoja, yliviivausta
(`~~teksti~~`) tai alaviitteitä ilman lisälaajennuksia generaattoriin.
