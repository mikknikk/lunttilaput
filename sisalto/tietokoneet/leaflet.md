---
title: Leaflet
---

Leaflet on kevyt JavaScript-kirjasto interaktiivisiin karttoihin —
avoimen lähdekoodin vaihtoehto esim. Google Maps -upotukselle, toimii
mm. OpenStreetMap-karttatiilillä ilman API-avainta.

## Peruskartan pystytys

```html
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
<div id="kartta" style="height: 400px;"></div>
```
`unpkg.com/leaflet` ilman versionumeroa osoittaa aina uusimpaan
julkaistuun versioon — tuotannossa kannattaa lukita tarkka versio
(esim. `leaflet@1.9.4/`), jotta päivitys ei riko sivustoa yllättäen.

```javascript
const kartta = L.map('kartta').setView([60.1699, 24.9384], 13);  // [lat, lon], zoom

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '&copy; OpenStreetMap-tekijät',
  maxZoom: 19
}).addTo(kartta);
```
URL-mallissa `{s}` = aliverkkotunnus, `{z}` = zoomaustaso, `{x}`/`{y}` =
tiilen koordinaatit, `{r}` (jos tuettu) = `@2x` retina-näytöille.

## Merkit (markers) ja popupit

```javascript
const merkki = L.marker([60.1699, 24.9384]).addTo(kartta);
merkki.bindPopup("Helsinki").openPopup();   // openPopup avaa heti, ei vasta klikkauksesta

// Popup ilman tiettyä merkkiä
L.popup()
  .setLatLng([60.1699, 24.9384])
  .setContent("Vapaa popup")
  .openOn(kartta);
```

## Muodot

```javascript
L.circle([60.17, 24.94], { radius: 500, color: 'red' }).addTo(kartta);   // säde metreinä
L.polygon([[60.17, 24.94], [60.18, 24.95], [60.16, 24.96]]).addTo(kartta);
L.polyline([[60.17, 24.94], [60.20, 25.00]]).addTo(kartta);
```

## Kerrokset (layers) ja niiden hallinta

```javascript
const kerrosryhma = L.layerGroup([merkki, L.marker([60.20, 25.00])]).addTo(kartta);
kartta.removeLayer(kerrosryhma);

L.control.layers({ "OSM": osmKerros }, { "Merkit": kerrosryhma }).addTo(kartta);
```

## GeoJSON

```javascript
fetch("alueet.geojson")
  .then(vastaus => vastaus.json())
  .then(data => {
    L.geoJSON(data, {
      style: feature => ({ color: feature.properties.vari }),
      onEachFeature: (feature, layer) => layer.bindPopup(feature.properties.nimi)
    }).addTo(kartta);
  });
```

## Tapahtumat

```javascript
kartta.on('click', e => {
  console.log(e.latlng);   // klikatun kohdan koordinaatit
});

merkki.on('click', () => merkki.openPopup());
```

## Omat ikonit

```javascript
const omaIkoni = L.icon({
  iconUrl: 'ikoni.png',
  iconSize: [32, 32],
  iconAnchor: [16, 32]     // piste, joka osoittaa tarkkaan sijaintiin
});
L.marker([60.17, 24.94], { icon: omaIkoni }).addTo(kartta);
```

## Rajaus näkymään (fit bounds)

```javascript
const ryhma = L.featureGroup([merkki1, merkki2, merkki3]);
kartta.fitBounds(ryhma.getBounds());   // zoomaa/keskitä niin että kaikki näkyvät
```
