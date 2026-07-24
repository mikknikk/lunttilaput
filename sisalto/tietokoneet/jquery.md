---
title: jQuery
---

**Ajankohtainen huomio:** jQuery ei ole "kuollut" — se pyörii yhä
valtaosassa WordPress-sivustoja (WordPress-ydin sisältää sen edelleen
taaksepäinyhteensopivuuden vuoksi) ja lukemattomissa vanhemmissa
järjestelmissä — mutta uusiin projekteihin sitä ei enää yleensä
suositella. Nykyiset selainten omat rajapinnat (`querySelector`,
`fetch`, `classList`, template literalit) kattavat suurimman osan syistä,
joiden takia jQuery aikanaan oli välttämätön (selainten epäyhtenäinen
DOM-käyttäytyminen). jQuery 4.0 on silti aktiivisesti ylläpidetty ja
poisti mm. vanhojen Internet Explorer -versioiden tuen.

## Valinta ja perusteet

```javascript
$(".luokka")           // CSS-valitsin, sama syntaksi kuin document.querySelectorAll
$("#id")
$("div").first()
$("li").eq(2)            // kolmas <li> (0-indeksoitu)
```

## DOM:n lukeminen ja muokkaus

```javascript
$(".otsikko").text();                  // hae tekstisisältö
$(".otsikko").text("Uusi teksti");       // aseta tekstisisältö
$(".sisalto").html("<b>HTML</b>");         // aseta HTML-sisältö
$("input").val();                            // hae lomakekentän arvo
$("input").val("oletusarvo");
$("img").attr("src", "kuva.png");
$(".elementti").addClass("aktiivinen");
$(".elementti").removeClass("piilotettu");
$(".elementti").toggleClass("valittu");
$(".laatikko").css("background-color", "red");
```

## Ketjutus (chaining)

```javascript
$(".elementti")
  .addClass("korostettu")
  .fadeIn(300)
  .delay(1000)
  .fadeOut(300);
```
jQuery-metodit palauttavat useimmiten saman jQuery-olion, joten
kutsuja voi ketjuttaa peräkkäin.

## Tapahtumat

```javascript
$(".nappi").on("click", function () {
  console.log("Klikattu");
});

$(".nappi").click(function () { /* lyhennemuoto .on("click", ...) */ });

$(document).on("click", ".dynaaminen", function () {
  // toimii myös elementeille, jotka lisätään DOM:iin vasta myöhemmin
});
```

## AJAX

```javascript
$.get("https://esimerkki.fi/api", function (data) {
  console.log(data);
});

$.ajax({
  url: "https://esimerkki.fi/api",
  method: "POST",
  data: { nimi: "Matti" },
  success: function (vastaus) { console.log(vastaus); },
  error: function (virhe) { console.error(virhe); }
});
```
Moderni vaihtoehto ilman jQueryä on selaimen sisäänrakennettu
`fetch()`-funktio (ks. JavaScript-lunttilappu) — uusissa projekteissa
suositeltavampi, koska ei vaadi koko jQuery-kirjaston latausta.

## Efektit

```javascript
$(".elementti").fadeIn();
$(".elementti").fadeOut();
$(".elementti").slideToggle();
$(".elementti").animate({ opacity: 0.5, left: "50px" }, 400);
```

## Dokumentin valmius

```javascript
$(document).ready(function () {
  // koodi ajetaan kun DOM on ladattu
});

$(function () {
  // lyhennemuoto samalle asialle
});
```

## Elementtien läpikäynti

```javascript
$("li").each(function (index, elementti) {
  console.log(index, $(elementti).text());
});
```
