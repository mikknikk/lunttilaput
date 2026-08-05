# lunttilaput

Sisältörepo `md-html-sivustogeneraattori`-generaattorille (erillinen repo,
todennäköisesti kloonattuna vierekkäin `/Users/mikko/Claude/`-hakemistossa).
Tämä repo sisältää VAIN sisältöä (`sisalto/`-kansio) ja julkaisu-workflown —
ei generointilogiikkaa. Ks. generaattorin oma `CLAUDE.md` arkkitehtuurista,
`index.md`-käytännöstä ja testausproseduurista — samat säännöt pätevät tässä
kirjoitettavaan sisältöön.

## Sisällön rakenne (`sisalto/`)

- **Kielet/** — kielenopiskelijan näkökulmasta kirjoitettuja numeroituja
  oppituntisarjoja (`kielet/<kieli>/00-johdanto.md`, `01-...md`, jne.) —
  ei yksittäisiä lunttilappuja. **Kahdeksanosainen rakenne**
  (`00-johdanto.md` ... `07-harjoituksia.md`, ks. mallina `kielet/
  indonesia/`) on järkevä OLETUS fraasikirjamaiselle kielisisällölle —
  näin kirjoitettiin alun perin kaikki viisi kieltä (espanja, hindi ja
  urdu, indonesia, japani, telugu) samassa commitissa, mutta se ei ole
  pysyvä rajoite: minkä tahansa kielen kurssi voi käyttää eri
  lukumäärää/rakennetta, jos syvempi tai muotoisesti erilainen
  pedagoginen lähestymistapa palvelee sitä aidosti paremmin.
  **telugu on tästä ensimmäinen esimerkki:** se käyttää nyt
  18-lukuista rakennetta (`00`...`17`), joka menee oikeaan
  kielioppisyvyyteen (verbien aikamuodot, kielto, sijamuotojärjestelmä,
  partisiipit, sukulaisuussanasto ja kohteliaisuusrekisteri), ja
  jokainen luku sisältää oppikirjamaisen lukukappaleen/dialogin, joka
  havainnollistaa kyseisen luvun kielioppia käytännössä. Tämä on
  dokumentoitu esimerkkinä, jota muut kielet voisivat seurata jos/kun
  niitä joskus vastaavasti syvennetään — ei vaatimuksena, että
  niidenkin täytyy. **Tärkeä periaate:** vieraalla kirjoitusjärjestelmällä
  kirjoitettavat kielet esitetään ensisijaisesti omalla skriptillään, ja
  mahdollinen translitteraatio noudattaa AINA virallista ISO-standardia
  silloin kun sellainen on olemassa — ei koskaan epävirallista
  romanisointia (esim. Hepburn japanille). Käytössä: ISO 15919
  (devanagari/hindi, telugu), ISO 3602/Kunrei-shiki (japani). Jos
  kielelle ei ole ISO-translitterointistandardia, OLETUS on jättää
  translitteraatio kokonaan pois — vain natiivi kirjoitusjärjestelmä.
  **Dokumentoitu poikkeus:** hindi ja urdu -kurssin urdu-sarakkeissa on
  käytössä projektikohtainen, ei-ISO- ja ei-ALA-LC-translitterointi
  (kuvattu kokonaan tiedostossa `sisalto/kielet/hindi-ja-urdu/
  01-kirjoitusjarjestelma.md`). Poikkeuksen perusteet: yhteinen
  hindi-urdu-kurssiformaatti hyötyy rinnakkaisesta translitteraatiosta,
  eikä mikään olemassa oleva standardi erottele urdun kirjaimia
  riittävän tarkasti — lähin kirjastostandardi ALA-LC yhdistää esim.
  kirjaimen ط ja retrofleksin ٹ samaksi romanisaatioksi. Tämä on
  poikkeus, ei uusi oletus: uutta ISO-standarditonta kieltä
  lisättäessä pätee edelleen oletus (vain natiivi kirjoitusjärjestelmä),
  ellei ole vastaavan vahvaa, dokumentoitua perustetta oman
  translitterointijärjestelmän lisäämiselle. Uutta kieltä lisättäessä
  käytä oletuksena kahdeksanosaista rakennetta ja samaa tarkkuutta
  translitteroinnissa, ellei kielelle ole hyvää syytä syventää
  rakennetta telugun tapaan.
- **Tietokoneet/** — jaettu aihepiirikohtaisiin alikategorioihin: Shellit,
  Päätteet, Editorit (sis. `vscode/`-alikansio kolmannella tasolla),
  Tekstinkäsittely, Paketinhallinta, Järjestelmä ja tietoturva, Web-kehitys,
  Ohjelmointikielet, Versionhallinta, Viestintä, Kuvankäsittely. Uusi
  lunttilappu sijoitetaan olemassa olevaan alikategoriaan aihepiirin mukaan,
  tai luodaan uusi alikategoria jos mikään ei sovi (ks. esimerkkinä
  `git log` -historia kategorioiden synnystä).
- **Videopelit/** — pelikohtaisia, kapeita käytännön apuvälineitä (ei
  läpipeluuohjeita).

## Kriittisin sääntö: tarkista faktat ennen kirjoittamista

Tämä on projektin tärkein toistuva laatuvaatimus. Ennen minkään täsmällisen
teknisen väitteen kirjoittamista (komennon täsmällinen syntaksi,
konfiguraatiotiedoston sijainti, versionumero, työkalun nykyinen
ekosysteemiasema kuten "onko X vielä käytössä/suositeltu"), **tarkista se
WebSearch/WebFetch-työkaluilla** — älä luota muistinvaraiseen tietoon, joka
voi olla vanhentunutta tai suoraan väärin. Tästä on ollut konkreettisia
esimerkkejä: väärät nano-näppäinsidonnat, puuttuva `-tls`-lippu irssin
palvelinesimerkissä, CentOS-version EOL-tilanne, yum→dnf-siirtymä,
iptables→nftables-siirtymä, jQueryn 2026-relevanssi. Kun aihe on hyvin
vakiintunut eikä muutu (esim. peruskielioppi, POSIX-työkalujen ikivanha
syntaksi), tarkistus ei ole yhtä kriittinen, mutta epävarmoissa tapauksissa
tarkista mieluummin liikaa kuin liian vähän.

## Front matter -käytäntö

```
---
title: Sivun otsikko
---
```
Jäsennin on naiivi merkkijonojaottelu, EI oikeaa YAML:ia — älä käytä
lainausmerkkejä `title`-arvon ympärillä (ne jäisivät kirjaimellisesti
näkyviin). Sivun otsikko ei toista kategorian nimeä (esim. "Git", ei
"Tietokoneet: Git") — kategoria näkyy jo navigaatiossa kontekstina.

## Julkaisu

`.github/workflows/deploy.yml` triggeröityy vain push:ista `sisalto/**`
-polkuun `main`-haarassa (tai manuaalisesti "Run workflow"). Pelkkä
generaattori-repon muutos (`@main`-viittaus) EI laukaise tätä workflow'ta
automaattisesti — jos haluat nähdä generaattoriin tehdyn muutoksen
tuotannossa heti, tarvitaan joko manuaalinen ajo tai pieni `sisalto/`-muutos.

## Git-työnkulku

Commitoi ja pushaa jokainen valmis lisäys/muutos erikseen (ei kerättyjä
isoja committeja), kuvaavalla viestillä joka mainitsee mitä testattiin.
