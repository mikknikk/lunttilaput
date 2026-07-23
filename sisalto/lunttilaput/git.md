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

## Haarat

```bash
git branch                  # listaa haarat
git switch -c uusi-haara    # luo ja vaihda uuteen haaraan
git switch main             # vaihda haaraan
git merge ominaisuus         # yhdistä haara nykyiseen
```

## Historia ja muutokset

```bash
git log --oneline
git diff                    # tallentamattomat muutokset
git diff --staged           # stagetut muutokset
git show <commit>
```

## Perumiset

| Komento | Kuvaus |
| --- | --- |
| `git restore tiedosto` | Kumoa tallentamattomat muutokset tiedostoon |
| `git restore --staged tiedosto` | Poista tiedosto stagelta |
| `git reset --soft HEAD~1` | Peru viimeinen commit, säilytä muutokset |
| `git revert <commit>` | Tee uusi commit, joka kumoaa toisen |

## Etärepot

```bash
git remote -v
git remote add origin git@github.com:org/repo.git
git fetch
```

## Yleisiä tilanteita

```bash
git stash          # laita muutokset syrjään väliaikaisesti
git stash pop       # palauta syrjään laitetut muutokset
git tag v1          # tägää nykyinen commit
git log --all --graph --oneline   # visuaalinen haarahistoria
```
