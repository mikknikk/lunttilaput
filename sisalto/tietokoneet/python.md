---
title: Python
---

## Muuttujat ja tyypit

```python
nimi = "Matti"          # str
ika = 30                  # int
hinta = 9.95               # float
aktiivinen = True          # bool
data = None

print(type(ika))          # <class 'int'>
```

## Merkkijonot

```python
nimi = "Maailma"
print(f"Hei, {nimi}!")           # f-string, suositeltu tapa
print("Hei, " + nimi + "!")      # yhdistäminen
print(nimi.upper())
print(len(nimi))
print(nimi.replace("a", "e"))
teksti = """
Monirivinen
merkkijono
"""
```

## Listat, tuplet, sanakirjat, joukot

```python
lista = ["omena", "banaani", "paaryna"]
lista.append("appelsiini")
lista[0]                    # "omena"
lista[-1]                   # viimeinen alkio
lista[1:3]                  # osaluettelo (slice)

tuple_ = (1, 2, 3)          # muuttumaton

sanakirja = {"nimi": "Matti", "ika": 30}
sanakirja["kaupunki"] = "Helsinki"
sanakirja.get("puuttuva", "oletus")

joukko = {1, 2, 3}          # ei kaksoiskappaleita, ei järjestystä
```

## Listakomprehensiot

```python
neliot = [x**2 for x in range(10)]
parilliset = [x for x in range(20) if x % 2 == 0]
sanakirja_comp = {x: x**2 for x in range(5)}
```

## Ehdot ja silmukat

```python
if ika >= 18:
    print("Täysi-ikäinen")
elif ika >= 13:
    print("Teini")
else:
    print("Lapsi")

for alkio in lista:
    print(alkio)

for i, alkio in enumerate(lista):
    print(i, alkio)

i = 0
while i < 5:
    i += 1
```

## Funktiot

```python
def tervehdi(nimi: str, tervehdys: str = "Hei") -> str:
    return f"{tervehdys}, {nimi}!"

print(tervehdi("Maailma"))
print(tervehdi("Maailma", tervehdys="Moi"))

# *args ja **kwargs mielivaltaiselle määrälle argumentteja
def summaa(*luvut):
    return sum(luvut)
```

## Luokat

```python
class Kayttaja:
    def __init__(self, nimi: str):
        self.nimi = nimi

    def tervehdi(self) -> str:
        return f"Hei, olen {self.nimi}"

kayttaja = Kayttaja("Maija")
print(kayttaja.tervehdi())
```

## Poikkeukset

```python
try:
    tulos = 10 / 0
except ZeroDivisionError as e:
    print(f"Virhe: {e}")
except Exception as e:
    print(f"Muu virhe: {e}")
else:
    print("Ei virheitä")
finally:
    print("Suoritetaan aina")
```

## Tiedostojen käsittely

```python
with open("tiedosto.txt", "r") as f:
    sisalto = f.read()

with open("tiedosto.txt", "w") as f:
    f.write("Uusi sisältö\n")
```
`with`-lause sulkee tiedoston automaattisesti, myös virhetilanteessa.

## Moduulit ja paketit

```python
import os
from datetime import datetime
import numpy as np           # tavanomainen lyhennealias

if __name__ == "__main__":
    print("Ajetaan suoraan skriptinä, ei importattuna")
```

## Virtuaaliympäristöt ja paketit

```bash
python3 -m venv .venv
source .venv/bin/activate      # macOS/Linux
.venv\Scripts\activate         # Windows

pip install paketti
pip freeze > requirements.txt
pip install -r requirements.txt
```

## Hyödyllisiä sisäänrakennettuja funktioita

```python
len(lista)
sorted(lista)
sum(luvut)
max(luvut) / min(luvut)
zip(lista1, lista2)
map(str, lista)
filter(lambda x: x > 0, luvut)
```
