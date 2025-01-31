---
# You can also start simply with 'default'
theme: ./theme
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /images/git-scm-icon.svg
# some information about your slides (markdown enabled)
title: "Webinaire Git : normer l’écriture des commits avec le « conventional commit »"
info: Produire un historique clair et créer un contexte favorable à l'automatisation
favicon: /images/favicon.png
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# Enable PDF generation
# download: true
---

# Normer l’écriture des commits avec le **conventional commit**

Un webinaire par Techno-low-gic

<a href="https://comprendre-git.com/fr/" target="blank">comprendre-git.com</a>

---

transition: fade-out
layout: image-right
image: /images/photo.webp

---

# Qui suis-je ?

Maxime Bréhin, 14 ans d’expérience avec Git, dont 8 ans en tant que formateur Git, JavaScript, React.

Un parcours professionnel varié : développeur, chef de projet, directeur technique, ingénieur R&D, formateur, entrepreneur.

Créateur de [Technolowgic](https://technolowgic.com/), pour l'accompagnement des entreprises et collectivités à l'éco-conception web et la sobriété numérique.

Militant pour un [numérique acceptable](https://louisderrac.com/numerique-acceptable/) et pour la résilience locale.

---

## layout: center

# Pourquoi normer les messages ?

<v-clicks>

- Clarifie la communication sur les évolutions du projet ;
- Facilite la contribution au projet ;
- Ouvre la voie à l’automatisation : changelog, montée de version logicielle.

</v-clicks>

---

# Exemple d’un historique sans règle ni convention

Même si une partie des contenus semble compréhensible, l’ensemble demande à être un peu plus clair et structuré.

```bash
| | * | c92597c2b - Add marketplace template and category link to categies (Simon J.)
| * | | d8d22b25f - formulaire de gestion des attribut/propriete pour les places de marche (Simon J.)
| * | | 3ddc8528f - Add marketplace template and category link to categies (Simon J.)
| |/ /
| * | e2183e07c - make admin work with multiple marketplace (Simon J.)
| * | 7004ee902 - add improt of marketplaceCategory (Simon J.)
| * | 41edd7e66 - remove some magic metaprograming in marketplace configuration (Simon J.)
| * | 123ae1da3 - add configuration for marketplace settings (Simon J.)
| * |   53823a407 - Merge branch 'marketplaces-v2' of super-project into marketplaces-v2 (Simon J.)
| |\ \
| | * | 7b5be0951 - Initialiseur autoloader des bridges Marketplaces (Jane D.)
| * | | c8775b384 - ajout de marketplace template et attribute pour representer les arborescence de de categorie cote mp (Simon J.)
| |/ /
| * | 11d466a59 - Socle fondamental Marketplaces v2, début d'implémentation templating PriceMinister (Jane D.)
* | | 5dc07160d - Calage sur dernier carrier-exports (Jane D.)
* | | 77b4cc10b - Recalage versions éparses/erronées dans submodule sale-channels et calage sur dernier g11n à jour (Jane D.)
* | | 49c8136a9 - Final tweaks pour l'intégration de la branche payment (Jane D.)
* | |   b5b95a6ea - Merge remote branch 'origin/payment' into v2 (Jane D.)
```

---

# _conventional commit_ : une convention parmi d'autres

Il ne s'agit pas de la seule convention existante. Beaucoup d'entreprises définissent encore leur propre modèle ou adaptent certains modèles existants.

Le _conventional commit_ offre le bénéfice de suivre une autre convention, **pour la numérotation logicielle** : le [Semantic Versioning](https://semver.org).

Cette convention défini 3 niveaux de numérotation :

> 1.0.32

Ces numéros ont les correspondances suivantes :

> MAJOR.MINOR.PATCH

<v-clicks>

Un patch est un correctif.

Une version mineur est l'ajout d'une fonctionnalité.

Une version majeure exprime une rupture de comptabilité.

</v-clicks>

---

# Les règles du _conventional commit_

Le modèle est simple :

```
<type>[contexte optionnel]: <description>

[corps optionnel]

[notes/pied de message optionnels]
```

---

# Contraintes des types

Le type est limité à une liste prédéfinie :

- **_feat_** : ajout/mise à jour de fonctionnalité ;
- **_fix_** : correction de bug ;
- **_docs_** : ajout/mise à jour de documentation ;
- **_style_** : modification de style et de mise en forme du code (espacements, virgules, etc.) ;
- **_refactor_** : modification des sources n’étant ni un correctif, ni un ajout de fonctionnalité ;
- **_perf_** : amélioration de la performance ;
- **_test_** : ajout ou correction de test ;
- **_build_** : modification affectant le “build” ou les dépendances externes (ex de contextes : webpack, npm) ;
- **_chore_** : autres mises à jour ne modifiant ni les sources, ni les tests ;
- **_ci_** : modification de la configuration ou des scripts liés à la CI (Travis, Circle, BrowserStack, etc.) ;
- **_revert_** : annuler (revert) un commit précédent.

---

# Renseigner un changement majeur

Pour indiquer un changement majeur, on utilisera soit le terme

> BREAKING CHANGE

en pied de message ou le suffixe `!` pour le type :

> chore!: drop support for Node 6

Le type n'a alors pas d'incidence.

---

# Garantir le respect de la convention

Tout à fait ! On peut :

- Assister la saisie au sein du projet avec un outil comme [commitizen](<https://comprendre-git.com/fr/automatisation/git-hooks-et-commitlint/#peut-on-%C3%AAtre-aid%C3%A9%C2%B7e-plut%C3%B4t-(et-plus-t%C3%B4t)-lors-de-l%E2%80%99%C3%A9criture-%3F>)
- Valider la saisie au moment de la finalisation du commit avec [commitlint](https://comprendre-git.com/fr/automatisation/git-hooks-et-commitlint/#installation-et-configuration)
- Valider les messages d'une branche avec commitlint, côté serveur Git

---

# Automatisation des releases

En configurant [Semantic Release](https://semantic-release.gitbook.io/semantic-release), on peut automatiser plusieurs choses, selon nos besoins :

<v-clicks>

- le calcul automatique de la **prochaine version logicielle** ;
- la **_release note_** ;
- un fichier `CHANGELOG.md` ;
- une publication sur une plateforme (exemple avec _npm_).

</v-clicks>

<v-click>

Voyons un exemple : https://gitlab.com/mbrehin/git-automated-release-demo/

</v-click>

---

## layout: end

# Merci

Besoin d'une [formation](https://comprendre-git.com/fr/formation/), d'être accompagné ?
Il suffit de demander !

<a href="mailto:contact@comprendre-git.com">contact@comprendre-git.com</a>

Tu peux aussi rejoindre [notre forum discord](https://discord.com/invite/Dbb9zt7jqe) pour poser tes questions et échanger sur les problématiques Git.

[comprendre-git.com](https://comprendre-git.com)
