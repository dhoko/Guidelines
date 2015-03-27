# Pour une CSS simple et réutilisable

## Introduction

Il est indispensable de ne pas coder pour soi-même mais, pour tous.
Une intégration doit pouvoir être repise par une autre personne sans la perdre, il doit y a voir de la logique.

Le mot d'ordre est [KISS](http://wikipedia.org/KISS) issu du monde unix. Puis DRY aussi.


## Table des matières

1. [Indentation](#1-indentation--)
2. [Commentaires](#2-commentaires--)
3. [Formatage](#3-formatage--)
4. [Quelques éléments indispensable](#4-quelques-%C3%A9l%C3%A9ments-indispensable--)
5. [Ecriture des classes](#5-ecriture-des-classes--)
6. [Préprocesseurs ?](#6-pr%C3%A9processeurs---)
7. [Le futur](#7-le-futur--)
8. [Quelques liens](#8-quelques-liens)

## Avant de commencer

- **Ne jamais styliser sur un id**
- **Ne jamais utiliser !important**
- **Ne jamais utiliser de style inline** (*A noter que l'approche pour du Natif, cf react-native est intéressante*)
- Ne jamais mettre de vendor prefix (*Laissons AutoPrefixer faire le boulôt*)
- Evitez les styles sur les tags
- Ne jamais mettre une seule typo dans une font-family
- Test all the things !
- Garder une spécificité moyenne de 10/20
- Pas de classes magiques (*text-align mis à part ainsi que float et clear: both*)
- Lire et imprimer ça :  [Learn CSS Specifishity with plankton, fish and sharks](http://www.standardista.com/wp-content/uploads/2012/01/specifishity1.pdf)

### Pourquoi ne pas styliser sur autre chose que des classes en général

La classe possède une spécificité faible *10* ce qui permet de repasser dessus aisément. L'ID étant à *100* c'est beaucoup plus difficile.

Bien sur grâce à la cascade on peut surcharger tout, même des `!importants`, mais ce n'est pas parceque l'on peut que l'on doit.

> Pour le cas du tag, le soucis ne provient pas de la spécificité mais de sa globalité. On stylise body html main mais pas plus.

La classe permet de garder un code maintenable.

## 1. Indentation

L'indentation doit se faire avec des **espaces**. Le tab doit contenir **2 espaces**.

> Pourquoi ? L'espace est fixe quelque soit l'env et l'éditeur. De plus pour copier son code dans Github, gist, jsfiddle, codepen etc. c'est pratique, on a le rendu attendu.

***On ne mélange pas les deux***

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

### Ordre de déclaration

Par ordre logique :

1. Le display
2. La taille
3. Les modifications tailles
4. Les background/couleurs
5. La typo

> Une piste [The Greatest tool for sorting CSS properties in specific order](http://csscomb.com/).

## 4. Quelques éléments indispensables

### Les guillemets pour les attributs

```css
// Mauvaise forme
[type=submit] {}

// Forme propre
[type="submit"] {}
```

Facilitons la lecture, mettons des doubles guillemets.

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

### Autres

- `-webkit-border-radius` **Non** [What CSS to prefix?](http://shouldiprefix.com/)
- `box-sizing: border-box` Amen. L'utiliser tu dois, pourquoi ? [box-sizing, et pourquoi pas ?](http://blog.goetter.fr/post/27612618411/box-sizing-et-pourquoi-pas)
- Pas de tailles dans line-height cf [Line-Height Units](http://tzi.fr/CSS/Text/line-height-units)
- Le PX m'a tuer. Préférons **em** ou mieux **rem** [Un petit pas pour l'em, un grand pas pour le web - Paris Web 2013](http://fr.slideshare.net/nhoizey/paris-web-2013-un-petit-pas-pour-lem-un-grand-pas-pour-le-web) et [Refonte de mon portfolio : du responsive tout en em](http://marieguillaumet.com/refonte-mon-portfolio-du-responsive-en-em-premiere-partie/)
- Les sélecteurs oui mais pas trop quand même. [MSIE 4095 Selector limit -- lol](http://www.habdas.org/msie-4095-selector-limit/)

> Une lecture sur les unités en CSS [Which CSS Measurements to use when](http://demosthenes.info/blog/775/Which-CSS-Measurements-To-Use-When)

## 5. Ecriture des classes

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

## 6. Préprocesseurs ?

Non.

## 7. Postprocesseurs ?

J'ai pour habitude de scinder mes CSS par modules et de concaténer tout.

Seulement si je veux faires des comportements pour toute mon app, je dois mettre un `_` devant le nom du fichier sinon il risque d'arriver après d'autres styles puis avec la cascade boum ça casse.

Solution: [PostCSS import](https://github.com/postcss/postcss-import) ou encore [CSSNext](https://github.com/cssnext/cssnext) si on veut faire du "CSS4".

## 8. Quelques liens

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

## 9. Remerciements

A vous :)
