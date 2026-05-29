# Markdown TOC Convention

## Rule

**Every Markdown file with more than 2 sections de premier niveau (`##`) doit avoir une Table des matières.**

- Le titre de la TOC est toujours `## Table des matières` (ancre : `#table-des-matières`)
- Les ancres sont basées sur les titres tels que générés par **VS Code** (voir règles ci-dessous)
- Chaque titre de section de premier niveau porte un lien retour `[↑](#table-des-matières)`

---

## Rationale

Les fichiers longs sans TOC sont difficiles à naviguer, notamment dans VS Code où le preview Markdown ne génère pas de navigation automatique. Une TOC normalisée + des liens retour permettent une navigation rapide dans les deux sens.

---

## Format des ancres (VS Code)

VS Code génère les ancres selon ces règles :
- Tout en minuscules
- Espaces → tirets `-`
- Caractères spéciaux supprimés (sauf tirets et lettres accentuées)
- Les accents sont **conservés** (ex. `é`, `è`, `à`)
- Les numéros de section sont inclus (ex. `## 1. Vue d'ensemble` → `#1-vue-densemble`)
- `--` double tiret conservé si présent dans le titre

### Exemples

| Titre | Ancre VS Code |
|-------|--------------|
| `## 1. Vue d'ensemble` | `#1-vue-densemble` |
| `## 2. Balisage — contrat HTML↔scripts` | `#2-balisage--contrat-htmlscripts` |
| `## Table des matières` | `#table-des-matières` |
| `## Scripts` | `#scripts` |
| `## Gestion de l'historique` | `#gestion-de-lhistorique` |

**Note :** GitHub utilise des règles différentes (les accents sont encodés en `%XX`). Cette convention cible VS Code uniquement.

---

## Format de la TOC

```markdown
## Table des matières

1. [Titre de la section 1](#ancre-1)
2. [Titre de la section 2](#ancre-2)
3. [Titre de la section 3](#ancre-3)
```

- Utiliser une liste numérotée (plus lisible pour des sections ordonnées)
- Une entrée par section de premier niveau (`##`) uniquement — pas les sous-sections (`###`)
- Placer la TOC juste après le titre principal (`#`) et une éventuelle description courte

---

## Lien retour vers la TOC

Chaque titre de section de premier niveau doit inclure un lien retour :

```markdown
## 1. Vue d'ensemble [↑](#table-des-matières)
```

- Lien placé à la fin du titre, séparé par un espace
- Symbole `↑` (U+2191)
- Ancre cible : `#table-des-matières` (fixe, quelle que soit la section)

---

## Critère d'audit

Un fichier Markdown **échoue** l'audit TOC si :
- Il contient **plus de 2 sections `##`** ET
- Il n'a pas de section `## Table des matières`, OU
- Les ancres de la TOC ne correspondent pas aux titres réels, OU
- Les titres de section ne portent pas de lien `[↑](#table-des-matières)`

---

## Keywords
markdown, TOC, table-des-matières, ancres, navigation, VS-Code, sections, liens-retour, convention
