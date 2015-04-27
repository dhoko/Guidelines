# Pour une CSS simple et réutilisable

## Introduction

Mot d'ordre ? [KISS](http://wikipedia.org/KISS)

## Table des matières

1. [Indentation](#1-indentation--)
2. [Commentaires](#2-commentaires--)
3. [Formatage](#3-formatage--)
4. [Quelques éléments indispensable](#4-quelques-%C3%A9l%C3%A9ments-indispensable--)
5. [Ecriture des classes](#5-ecriture-des-classes--)
6. [Préprocesseurs ?](#6-pr%C3%A9processeurs---)
7. [Le futur](#7-le-futur--)
8. [Quelques liens](#8-quelques-liens)

## TL;DR

- On ne stylise pas avec
  - un id
  - `!important`
  - du style inline
- On évite les styles sur des tas
- On ne met pas de choses inutiles comme les préfixes dans sa CSS
- Garder une spécificité moyenne de 10/20
- Pas de classes magiques (*.left, .right, .center, .mp*)
- Lire et imprimer ça :  [Learn CSS Specifishity with plankton, fish and sharks](http://www.standardista.com/wp-content/uploads/2012/01/specifishity1.pdf)


## 1. Indentation

On indente avec des **espaces**, on obtient donc: 1 tab = 2 espaces.

> Pourquoi ? L'espace est fixe quelque soit l'env et l'éditeur. De plus pour copier son code dans Github, gist, jsfiddle, codepen etc. c'est fiable, on a le rendu attendu.

> *On ne mélange pas les deux*

> PS 1 : pensez à configurer votre éditeur comme SublimeText pour qu'il enregistre vos fichiers avec des espaces automatiquement.

> PS 2 : regardez du côté d'[EditorConfig](http://editorconfig.org/), ça permet de définir des conventions de codages suivant le type du fichier sur lequel nous sommes en train de travailler.

## 2. Commentaires

> Dans les dix commandements on peut trouver: "Ton code tu commenteras"

## 3. Formatage

- Un espace entre le nom du tag/sélecteur et l'accolade ouvrante
- Retour à la ligne après chaque propriété
- Pas de point virgule pour la dernière propriété
- Toujours des doubles guillemets pour les sélecteurs d'attributs
- Indentation de 2 espaces avant chaque propriété
- Pas d'espace entre la propriété et le :
- Un espace après le :
- Pas d'inline si > 2 propriétés
- Un saut de ligne entre deux styles

On obtient donc :

```css
input[type="checkbox"]:checked + div {
  border-color: #bada55;
  background-color: #c0ff33;
  opacity: 1
}
```

### Les unités inutiles

Inutile de mettre des unités quand nous mettons une propriété à zéro:

```css
border: 0px; /* Nop */
border: 0; /* Oui */
```

De même pour les valeurs décimales:

```css
font-size: 0.4em; /* Nop */
font-size: .4em; /* Oui */
```

### Ordre de déclaration

Par ordre logique :

1. Le display
2. La taille
3. Les modifications tailles
4. Les background/couleurs
5. La typo

> Une piste [The Greatest tool for sorting CSS properties in specific order](http://csscomb.com/).


### Autres

- `box-sizing: border-box` Amen. L'utiliser tu dois, pourquoi ? [box-sizing, et pourquoi pas ?](http://blog.goetter.fr/post/27612618411/box-sizing-et-pourquoi-pas)
- Pas de tailles dans line-height cf [Line-Height Units](http://tzi.fr/CSS/Text/line-height-units)
- Le PX m'a tuer. Préférons **em** ou mieux **rem** [Un petit pas pour l'em, un grand pas pour le web - Paris Web 2013](http://fr.slideshare.net/nhoizey/paris-web-2013-un-petit-pas-pour-lem-un-grand-pas-pour-le-web) et [Refonte de mon portfolio : du responsive tout en em](http://marieguillaumet.com/refonte-mon-portfolio-du-responsive-en-em-premiere-partie/)
- Les sélecteurs oui mais pas trop quand même. [MSIE 4095 Selector limit -- lol](http://www.habdas.org/msie-4095-selector-limit/)

> Une lecture sur les unités en CSS [Which CSS Measurements to use when](http://demosthenes.info/blog/775/Which-CSS-Measurements-To-Use-When)

## 4. Ecriture des classes

```
.[namespace]-{container|figure|?}-{item,type,object}-flag
```

- *namespace*: Le type de module sur lequel votre CSS s'applique
- *{container|figure|?}*: Le niveau/typage du module
- *{item,type,object}*: Le type d'élément (titre etc.)
- *flag*: succes,error,solde etc.

> On peut avoir jusqu'a deux typages de modules

##### Exemple:

```css
.grid-container {}
.grid-container-item {}
.grid-container-item-odd {}

/*
  Namespace = shopList
  Typage 1 = info
  Typage 2 = container
 */
.shopList-info-container {}
.shopList-info-container-title {}
```

##### Précisions

Il est d'usage de définir,
  - les li d'utiles liste ainsi: `namespace-item`
  - les containers de liste: `namespace-container`
  - les figure (contenant une image): `namespace-figure`
  - l'image dans une figure': `namespace-figure-item`
  - la figcaption dans une figure': `namespace-figure-legend`

> *Le type d'objet n'est pas obligatoire, on peut avoir toggle qui est un flag après le typage de module.*


### Sélecteurs

On utilise beaucoup les attributs cf [The Skinny on CSS Attribute Selectors](http://css-tricks.com/attribute-selectors/). Pourquoi ?

- Factorisation du code
- Poid minime
- Evite de mettre des classes de partout
- Si on respecte les conventions c'est simple et léger
- Pas de CSS trop longues

> Par contre c'est nettement moins accessible et moins lisible.

#### Exemple:

```css
[class^="btn-kaction-"] {
    display: inline-block;
    width: 1em;
    height: 1em;
    border: 0;
    background-color: transparent;
    background-repeat: no-repeat;
    vertical-align: top;
    text-indent: -9999px
}

.btn-kaction-edit {background-image: url(/static/images/picto/edit.png)}
.btn-kaction-delete {background-image: url(/static/images/picto/bin.png)}
.btn-kaction-duplicate {background-image: url(/static/images/picto/duplicate.png)}
.btn-kaction-password {background-image: url(/static/images/picto/password.png)}
```

On a ici un exemple de boutons qui sont simple à enrichir, pour tous.

### Specificité

En moyenne entre 10/20, il est préférable de ne pas dépasser un attribut ou une classe sur un sélecteurs. Restons simple et léger.

## 5. Préprocesseurs ?

Non.

## 6. Postprocesseurs ?

J'ai pour habitude de scinder mes CSS par modules et de concaténer tout.

Seulement si je veux faires des comportements pour toute mon app, je dois mettre un `_` devant le nom du fichier sinon il risque d'arriver après d'autres styles puis avec la cascade boum ça casse.

Solution: [PostCSS import](https://github.com/postcss/postcss-import) ou encore [CSSNext](https://github.com/cssnext/cssnext) si on veut faire du *"CSS4"*.

### Découpage

Voilà un fichier `index.css` que j'utilise avec [PostCSS import](https://github.com/postcss/postcss-import).

```css
@import 'common.css';
@import 'buttons.css';

/* UI modules */
@import 'ui/sidebarRwd.css';
@import 'ui/grid.css';

/* Modules */
@import 'modules/cartList.css';
@import 'modules/navBar.css';

/* Pages */
@import 'pages/home.css';
@import 'pages/login.css';
```

L'arborescence qui va avec:

```shell
.
├── common.css
├── buttons.css
├── ui
    ├── sidebarRwd.css
    └── grid.css
├── modules
    ├── cartList.css
    └── navBar.css
└── pages
    ├── home.css
    └── login.css
```

### Fonctionnement

Ce qui est dans `common.css`, c'est ce qui est global, on y trouve des styles sur certains tag comme le a. Ou encore le fonctionnement de mon wrapper.

Dans les modules ui, ce sont des classes qui vont pouvoir être utilisés ailleurs. Design de base et surtout de la structure.

Dans les modules, ce sont chaques composants de mes sites/applications. Tout est granulaire donc une CSS par composant. Chaque fichier est léger et est responsable de son évolution à travers les différentes tailles de viewport.

Dans les pages ce sont des styles spécifiques pour une page. C'est une surcouche au cas ou. J'ai toujours une classe `(state|page)-<nom de ma page>` dans mon body, pour ça. Ca apporte un confort pas franchement indispensable, mais parfois utile.


## 6. Quelques liens

### Articles techniques

- [Absolute Horizontal And Vertical Centering In CSS](Absolute Horizontal And Vertical Centering In CSS)
- [Cat CSS box model](http://www.flickr.com/photos/cmdshiftdesign/5910326877/) Les chats et le CSS, une réussite.
- [Ce que vous avez toujours voulu savoir sur CSS](http://iamvdo.me/conf/2013/kiwiparty/#/)
- [A Couple of Use Cases for Calc()](http://css-tricks.com/a-couple-of-use-cases-for-calc/)
- [Le modèle de boite flexible en CSS 3](http://jeremie.patonnier.net/post/2009/11/10/Le-modele-de-boite-flexible-en-CSS-3)

### Quelques outils

- [AutoPrefixer](https://github.com/ai/autoprefixer) pour les préfixes en se basant sur l'excellent [Can I use...](http://caniuse.com/). Il existe aussi une tâche grunt [grunt-autoprefixer](https://github.com/nDmitry/grunt-autoprefixer).
- [:nth-tester](http://css-tricks.com/examples/nth-child-tester/) Car nth-child ce n'est forcément ce qui est le plus intuitif.
- [CSS3 structural pseudo-class selector tester](http://lea.verou.me/demos/nth.html?) pour jouer et comprendre nth-*
- [Flexy boxes](http://the-echoplex.net/flexyboxes/) Pour les flexbox
- [CSSCSS](http://zmoazeni.github.io/csscss/) Pour voir la redondance au sein de votre CSS
- [Em Baseline Generator](http://joshnh.com/tools/em-baseline-generator.html) Car l'em c'est bon pour la santé.
- [CSS Almanac](http://css-tricks.com/almanac/) Pour comprendre ce que sont les sélecteurs CSS et qui sont-ils. Idem pour les propriétés.
- [What CSS to prefix?](http://shouldiprefix.com/) Can I use version user-friendly
- [CSS Compatibility and Internet Explorer](http://msdn.microsoft.com/en-us/library/cc351024.aspx) un classique à garder

## 97. Remerciements

A vous :)
