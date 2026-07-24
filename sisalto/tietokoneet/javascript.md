---
title: JavaScript
---

## Muuttujat

```javascript
let nimi = "Matti";      // uudelleensidottava, lohko-scope
const ika = 30;            // ei uudelleensidottava, lohko-scope
var vanha = "vältä";        // funktio-scope, historiallinen — vältä uudessa koodissa
```

## Tyypit ja vertailu

```javascript
typeof "teksti"     // "string"
typeof 42             // "number"
typeof true             // "boolean"
typeof undefined          // "undefined"
typeof null                 // "object" (historiallinen kummallisuus JS:ssä)

1 === "1"    // false — tiukka vertailu, ei tyyppimuunnosta
1 == "1"      // true — löysä vertailu, tekee tyyppimuunnoksen (vältä)
```

## Merkkijonot

```javascript
const nimi = "Maailma";
console.log(`Hei, ${nimi}!`);         // template literal, suositeltu tapa
console.log("Hei, " + nimi + "!");     // yhdistäminen
"Hei".toUpperCase();
"Hei".length;
"Hei maailma".split(" ");
```

## Taulukot

```javascript
const lista = ["omena", "banaani", "paaryna"];
lista.push("appelsiini");           // lisää loppuun
lista.map(x => x.toUpperCase());     // uusi taulukko, jokainen alkio muokattu
lista.filter(x => x.length > 5);      // uusi taulukko, vain ehdon täyttävät
lista.reduce((acc, x) => acc + x.length, 0);  // yhdistä yhdeksi arvoksi
lista.find(x => x.startsWith("b"));    // ensimmäinen täsmäävä alkio
lista.includes("omena");                // sisältääkö taulukko arvon
const [eka, toka, ...loput] = lista;      // destrukturointi
```

## Oliot

```javascript
const kayttaja = { nimi: "Matti", ika: 30 };
kayttaja.nimi;                 // piste-notaatio
kayttaja["nimi"];               // hakasulkeet (hyödyllinen dynaamiseen avaimeen)
const { nimi, ika } = kayttaja;  // destrukturointi
const kopio = { ...kayttaja, kaupunki: "Helsinki" };  // spread: kopio + lisäys
```

## Funktiot

```javascript
function tervehdi(nimi) {
  return `Hei, ${nimi}!`;
}

const tervehdiNuoli = (nimi) => `Hei, ${nimi}!`;   // arrow function, lyhyempi
const oletusarvo = (nimi = "Maailma") => `Hei, ${nimi}!`;

function summaa(...luvut) {          // rest-parametri: mielivaltainen määrä argumentteja
  return luvut.reduce((a, b) => a + b, 0);
}
```
Arrow function ei sido omaa `this`-arvoaan — se perii ympäröivän
kontekstin `this`:n, mikä on usein juuri toivottua (esim. luokkien
sisällä).

## Ehdot ja moderni syntaksi

```javascript
const arvo = kayttaja?.osoite?.katu;         // optional chaining: ei virhettä jos väliarvo puuttuu
const nimi2 = kayttaja.nimi ?? "Tuntematon";   // nullish coalescing: oletus vain null/undefined-tapauksessa
const tulos = ika >= 18 ? "täysi-ikäinen" : "alaikäinen";
```

## Luokat

```javascript
class Kayttaja {
  constructor(nimi) {
    this.nimi = nimi;
  }

  tervehdi() {
    return `Hei, olen ${this.nimi}`;
  }
}

class Admin extends Kayttaja {
  tervehdi() {
    return `${super.tervehdi()} (admin)`;
  }
}
```

## Asynkroninen koodi

```javascript
fetch("https://esimerkki.fi/api")
  .then(vastaus => vastaus.json())
  .then(data => console.log(data))
  .catch(virhe => console.error(virhe));

async function hae() {
  try {
    const vastaus = await fetch("https://esimerkki.fi/api");
    const data = await vastaus.json();
    console.log(data);
  } catch (virhe) {
    console.error(virhe);
  }
}
```
`async/await` on syntaktista sokeria Promisejen päällä — helpompi lukea
kuin pitkä `.then()`-ketju, mutta toimii samalla mekanismilla.

## Moduulit (ES-moduulit)

```javascript
// tiedosto.js
export function tervehdi() { /* ... */ }
export default class Kayttaja { /* ... */ }

// toinen-tiedosto.js
import Kayttaja, { tervehdi } from "./tiedosto.js";
```

## DOM-perusteet

```javascript
document.querySelector(".luokka");        // ensimmäinen täsmäävä elementti
document.querySelectorAll("div");           // kaikki täsmäävät (NodeList)
elementti.addEventListener("click", () => { /* ... */ });
elementti.classList.add("aktiivinen");
elementti.textContent = "Uusi teksti";
```
