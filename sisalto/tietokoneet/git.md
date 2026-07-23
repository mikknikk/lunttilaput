---
title: Git
---

## Perusworkflow

```bash
git status
git add tiedosto
git commit -m "Viesti"
git push
git pull
```

## Alustus ja kloonaus

```bash
git init
git clone git@github.com:org/repo.git
git clone --depth 1 git@github.com:org/repo.git   # pinnallinen kloonaus
```

## Haarat

```bash
git branch                  # listaa haarat
git switch -c uusi-haara    # luo ja vaihda uuteen haaraan
git switch main             # vaihda haaraan
git merge ominaisuus         # yhdistä haara nykyiseen
git branch -d haara          # poista yhdistetty haara
git branch -D haara          # poista pakolla
```

## Historia ja muutokset

```bash
git log --oneline
git log --all --graph --oneline   # visuaalinen haarahistoria
git log -- tiedosto                # tiedoston historia
git blame tiedosto                 # kuka muutti minkäkin rivin
git diff                    # tallentamattomat muutokset
git diff --staged           # stagetut muutokset
git show <commit>
```

## Perumiset

| Komento | Kuvaus |
| --- | --- |
| `git restore tiedosto` | Kumoa tallentamattomat muutokset tiedostoon |
| `git restore --staged tiedosto` | Poista tiedosto stagelta |
| `git reset --soft HEAD~1` | Peru viimeinen commit, säilytä muutokset stagettuna |
| `git reset --mixed HEAD~1` | Peru commit, säilytä muutokset stagettamattomana |
| `git reset --hard HEAD~1` | Peru commit ja hylkää muutokset kokonaan |
| `git revert <commit>` | Tee uusi commit, joka kumoaa toisen (turvallinen jaetulle haaralle) |
| `git reflog` | Näytä HEAD:n liikkeet — pelastusrengas väärän resetin jälkeen |

## Rebase ja historian siistiminen

```bash
git rebase main                    # siirrä haaran commitit mainin päälle
git rebase -i HEAD~3                # muokkaa/yhdistä 3 viimeistä commitia
git cherry-pick <commit>            # tuo yksittäinen commit toisesta haarasta
git commit --amend                  # muokkaa viimeisintä committia
```

Älä rebasea haaraa, jota muut jo käyttävät — historian uudelleenkirjoitus
rikkoo heidän kloonauksensa.

## Etärepot

```bash
git remote -v
git remote add origin git@github.com:org/repo.git
git fetch                   # hae muutokset ilman yhdistämistä
git push -u origin haara     # pushaa ja aseta seurattava haara
git push --force-with-lease  # turvallisempi force-push (tarkistaa etätilan)
```

## Stash

```bash
git stash            # laita muutokset syrjään väliaikaisesti
git stash pop         # palauta viimeisin ja poista pino
git stash list        # listaa kaikki tallennetut
git stash apply stash@{1}   # palauta tietty, älä poista pinosta
```

## Vianetsintä

```bash
git bisect start
git bisect bad                # nykyinen commit on viallinen
git bisect good v1.0          # tämä vanha commit toimi
# git testaa binäärihaulla väliin jääviä commiteja, merkitse jokainen
# `git bisect good` tai `git bisect bad`, kunnes syyllinen löytyy
git bisect reset
```

## Alimoduulit ja worktreet

```bash
git submodule add git@github.com:org/kirjasto.git polku/kirjasto
git submodule update --init --recursive

git worktree add ../toinen-haara haara-nimi   # toinen työhakemisto samasta repostä
```

## Tägit

```bash
git tag v1
git tag -a v1 -m "Ensimmäinen julkaisu"   # annotoitu tägi
git push --tags
```

## .gitignore ja siivous

```
# .gitignore-esimerkki: tiedostot/kansiot, joita git ei koskaan seuraa
*.log
build/
!build/pidettava.txt   # huutomerkki = poikkeus säännöstä
```

```bash
git clean -n     # näytä mitä poistettaisiin (kuivaharjoittelu)
git clean -fd     # poista seuraamattomat tiedostot ja kansiot
```

## Hyödyllisiä aliaksia

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.lg "log --oneline --graph --all"
```
