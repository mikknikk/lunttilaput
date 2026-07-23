---
title: PHP
---

## Perusrakenne

```php
<?php
echo "Hei maailma\n";
?>
```
Sulkeva `?>` voidaan jättää pois, jos tiedosto sisältää pelkkää PHP:ta —
tämä välttää vahingossa tulostuvat rivinvaihdot tiedoston lopussa.

## Muuttujat ja tyypit

```php
$nimi = "Matti";       // merkkijono
$ika = 30;              // kokonaisluku
$hinta = 9.95;          // liukuluku
$aktiivinen = true;     // totuusarvo
$data = null;

var_dump($nimi);        // näytä arvo ja tyyppi
echo gettype($ika);     // "integer"
```

## Merkkijonot

```php
$nimi = "Maailma";
echo "Hei, $nimi!";          // muuttuja tulkitaan kaksoislainauksissa
echo 'Hei, $nimi!';           // ei tulkita yksinkertaisissa lainauksissa
echo "Hei, " . $nimi . "!";   // yhdistäminen pisteellä
echo strtoupper($nimi);
echo strlen($nimi);
echo str_replace("a", "e", $nimi);
```

## Taulukot

```php
$lista = ["omena", "banaani", "paaryna"];
$assoc = ["nimi" => "Matti", "ika" => 30];

foreach ($lista as $alkio) {
    echo $alkio . "\n";
}

foreach ($assoc as $avain => $arvo) {
    echo "$avain: $arvo\n";
}

$lista[] = "appelsiini";     // lisää alkio
count($lista);                 // alkioiden määrä
```

## Ehdot ja silmukat

```php
if ($ika >= 18) {
    echo "Täysi-ikäinen";
} elseif ($ika >= 13) {
    echo "Teini";
} else {
    echo "Lapsi";
}

for ($i = 0; $i < 5; $i++) {
    echo $i;
}

while ($ehto) {
    // ...
}

$tulos = $ika >= 18 ? "kyllä" : "ei";   // ternäärioperaattori
```

## Funktiot

```php
function tervehdi(string $nimi, string $tervehdys = "Hei"): string {
    return "$tervehdys, $nimi!";
}

echo tervehdi("Maailma");
echo tervehdi("Maailma", "Moi");
```

## Assosiatiiviset rakenteet ja null-turvallisuus

```php
$arvo = $data['avain'] ?? "oletusarvo";   // null coalescing -operaattori
$data['avain'] ??= "asetettu vain jos puuttuu";
```

## Luokat

```php
class Kayttaja {
    public string $nimi;

    public function __construct(string $nimi) {
        $this->nimi = $nimi;
    }

    public function tervehdi(): string {
        return "Hei, olen {$this->nimi}";
    }
}

$kayttaja = new Kayttaja("Maija");
echo $kayttaja->tervehdi();
```

## Poikkeukset

```php
try {
    if (!$tiedosto) {
        throw new Exception("Tiedostoa ei löytynyt");
    }
} catch (Exception $e) {
    echo "Virhe: " . $e->getMessage();
} finally {
    echo "Suoritetaan aina";
}
```

## Composer (riippuvuuksienhallinta)

```bash
composer init
composer require vendor/paketti
composer install
composer update
```
`composer.json` kuvaa projektin riippuvuudet, `vendor/autoload.php`
ladataan yleensä tiedoston alussa autoloadauksen käyttöön ottamiseksi.

## Palvelimen käynnistys kehitystä varten

```bash
php -S localhost:8000
```
