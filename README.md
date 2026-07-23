# lunttilaput

Tämä repo sisältää vain sisällön (Markdown-tiedostot `sisalto/`-kansiossa).
Rakenne, ulkoasu ja generointilogiikka elävät erillisessä
`md-html-sivustogeneraattori`-repossa, jota tämän repon GitHub Actions -workflow
kutsuu.

## Uuden sivun lisääminen

1. Lisää `.md`-tiedosto sopivaan alikansioon `sisalto/`-kansion alle (uusi
   alikansio = uusi kategoria navigaatiossa).
2. Aloita tiedosto front matterilla:
   ```
   ---
   title: Sivun otsikko
   ---
   ```
3. Committaa ja pushaa `main`-haaraan. GitHub Actions generoi sivuston ja vie
   sen palvelimelle automaattisesti.

## Käyttöönotto (kertaluontoiset asetukset)

1. Julkaise `md-html-sivustogeneraattori`-repo `main`-haaraan.
2. Päivitä `.github/workflows/deploy.yml` viittaamaan oikeaan
   organisaatioon/repoon (`uses: <org>/md-html-sivustogeneraattori@main`).
   `@main` tarkoittaa, että workflow käyttää aina generaattorin uusinta
   versiota — jos generaattoriin tehty muutos rikkoo jotain, se vaikuttaa
   heti tähänkin sivustoon.
3. Lisää tämän repon Settings → Secrets and variables → Actions:
   - `DEPLOY_SSH_KEY` — yksityinen SSH-avain, jolla on kirjoitusoikeus vain
     kohdehakemistoon palvelimella
   - `DEPLOY_HOST` — palvelimen osoite
   - `DEPLOY_USER` — käyttäjätunnus
   - `DEPLOY_TARGET_DIR` — kohdekansio palvelimella (esim. `/var/www/luntti/`)
4. Varmista, että palvelimella on staattinen web-palvelin (esim. nginx)
   tarjoilemassa `DEPLOY_TARGET_DIR`-kansiota. Palvelimelle ei tarvitse
   asentaa Pythonia, gitiä eikä muita build-työkaluja.

## Paikallinen esikatselu

```bash
pip install markdown
python3 ../md-html-sivustogeneraattori/build.py \
  --content sisalto --output _site --templates ../md-html-sivustogeneraattori/templates \
  --site-title "Ohjeet ja lunttilaput"
cd _site && python3 -m http.server 8000
```
