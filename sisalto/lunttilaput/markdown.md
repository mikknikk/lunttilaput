---
title: Markdownin lunttilappu
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
| `~~yliviivaus~~` | yliviivaus (jos tuettu) |
| `` `koodi` `` | `koodi` |

## Listat

```
- Kohta 1
- Kohta 2
  - Alakohta

1. Ensimmäinen
2. Toinen
```

## Linkit ja kuvat

```
[Linkin teksti](https://esimerkki.fi)
![Kuvan vaihtoehtoinen teksti](kuva.png)
```

## Lainaukset

```
> Tämä on lainaus.
> Se voi jatkua usealle riville.
```

## Koodilohkot

Kolmen backtickin väliin, valinnaisella kielimerkinnällä:

````
```python
print("Hei maailma")
```
````

## Taulukot

```
| Sarake 1 | Sarake 2 |
| --- | --- |
| Arvo A | Arvo B |
```

## Vaakaviiva

```
---
```

## Vinkki tälle sivustolle

Jokaisen `.md`-tiedoston alussa voi olla front matter, joka määrittää sivun
otsikon:

```
---
title: Sivun otsikko
---
```
