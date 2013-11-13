# Pour une CSS simple et réutilisable

Ce document a pour but de définir une liste de recommandations pour permettre une intégration simple et compréhensible.

Ce document est destiné avant tout à servir au sein de mon équipe dans mon travail. Ce n'est pas gravé dans le marbre, sauf pour les personnes travaillant directement avec moi sur de l'intégration au sein de [Procheo](http://procheo.fr).

Merci de bien vouloir contribuer.

Exprimez vos idées, vos interrogations et vos remarques en bien ou en mal


## Introduction

Une intégration ce n'est pas facile, c'est en partant ainsi que l'on risque de faire de gros dégâts. C'est pareil pour les CSS, ce n'est pas parce qu'il n'y a pas de logique comme dans un langage du genre, JavaScript, C etc. que c'est simple.

Déjà, le 'if' nous avons ( *pseudo-classes etc.* ), le calcul ça arrive ( *calc* ), etc. On ne va pas tout lister, il y a de quoi faire. Quoi qu'il en soit le langage est simple, mais on fait très vite n'importe quoi. Résultat ?

- Des CSS > 2000 lignes
- 15 000 sélécteurs
- !important
- #lol #de abbr#feu b.titanic + .iceberg {float : none }
- 43,43px
- -ms-* (pour une intégration dédié Webkit -- Webkit m'a tuer)
- etc.

Devant ces cancers, nous autres intégrateurs nous devons apporter des soins. La cascade c'est de l'art, pas un truc qui fait chier donc on met un `!important`.

Une intégration doit facilement pouvoir évoluer et pouvoir et changer de mains, sans pour autant perdre le dev ou l'intégrateur.

Le mot d'ordre est [KISS](http://wikipedia.org/KISS) issu du monde unix. Puis au passage DRY aussi.


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
- Ne jamais mettre une seule typo dans une font-family
- Test de la typo sur un navigateur = tester une intégration dans Chrome et dire ok pour IE6
- Le moins possible de classes magiques et atomique (sauf 1 cas : les grilles cf, [960.gs](http://960.gs))
- Lire et imprimer ça :  [Learn CSS Specifishity with plankton, fish and sharks](http://www.standardista.com/wp-content/uploads/2012/01/specifishity1.pdf)

### Pourquoi on ne stylise pas sur un id ou avec !important

Ils possèdent tous les deux une spécificité trop importante. Passer dessus un id on peut aisément. Mais pour !important, gloups (déjà vu hélas...).

Un id étant unique, très peu d'éléments sont susceptibles d'avoir un style avec id, car ça veut dire un truc qui n'est jamais dupliqué ( *un logo dans le header on peut imaginer* ). Une fois que l'on maitrise le contexte on peut styliser un id.

Par contre, pour `!important`, il n'y a pas de négociation. Non, je pense même que mettre un !important dans sa CSS montre que celle-ci est mal pensée.


## 1. Indentation

Identons avec des **espaces**, avec un tab qui vaut 4 espaces. Le code en est plus clair et lisible.

De plus l'espace passe partout quel que soit le support et l'éditeur ou le site ( *copions du code dans une issue Github tab vs espaces* ).

***On ne mélange pas les deux***

> PS 1 : pensez à configurer votre éditeur comme SublimeText pour qu'il enregistre vos fichiers avec des espaces automatiquement.

> PS 2 : regardez du côté d'[EditorConfig](http://editorconfig.org/), ça permet de définir des conventions de codages suivant le type du fichier sur lequel nous sommes en train de travailler.

## 2. Commentaires

Quel que soit le projet : *un code sans commentaires ne vaut rien*.

Il n'y a pas d'argument recevable si ce n'est, une issue de 3 écrans pour vous expliquer pourquoi on commente, comment et avec quel outil ( *travailler avec moi est très drôle* ).

Revenons à nos moutons, en CSS nous ne commentons pas tout et pas n'importe comment. Nous faisons ici du **commentaire de zone**. Les classes doivent être assez expressives pour permettre ceci ( *encore un coup contre le CSS atomique* ).


```css
/***********************
*
*    Header
*
************************/

.header {
    height: 150px;
    background: #bada55
}

.header ul li {display: inline-block} // Spéciale dédicasse à IE

.header::before {
    content: '42'
}
```

Sinon en plein milieu de votre code, un commentaire classique suffit :

```css
.post-content {
    padding: 2px 4px;

    /* Un peu de magie */
    margin-left: 13,37px

    border-color: #c0ffee
}
```

Le fait de sauter une ligne avant et après peut mettre en valeur ce commentaire.

## 3. Formatage

- Un espace entre le nom du tag/sélecteur et l'accolade ouvrante
- Retour à la ligne après chaque propriété
- Pas de point virgule pour la dernière propriété
- Toujours des doubles guillemets pour les sélecteurs d'attributs
- Indentation de 4 espaces avant chaque propriété
- Pas d'espace entre la propriété et le :
- Un espace après le :
- Pas d'inline si > 2 propriétés
- Un saut de ligne entre deux styles

On obtient donc :

```css
input[type="checkbox"]:checked + div {
    border-color: #bada55;
    background-color: #676767;
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

Après ceci est une recommandation, on peut également le faire avec un ordre alphabétique. Ce n'est pas le plus important en soi, car c'est quelque chose que l'on peut nettoyer par la suite.

> Une piste [The Greatest tool for sorting CSS properties in specific order](http://csscomb.com/) ou alors il doit surement exister une tâche pour Grunt.

## 4. Quelques éléments indispensables

- `[type=submit]` = non préférez une structure propre : `[type="submit"]`
- `border:0px` = non l'unité est inutile ici -> `border: 0`
- `-webkit-border-radius` **Non** [What CSS to prefix?](http://shouldiprefix.com/)
- `box-sizing: border-box` Amen. L'utilsier tu dois, pourquoi ? [box-sizing, et pourquoi pas ?](http://blog.goetter.fr/post/27612618411/box-sizing-et-pourquoi-pas)
- Pas de tailles dans line-height cf [Line-Height Units](http://tzi.fr/CSS/Text/line-height-units)
- Le PX m'a tuer. Préférons **em** ou mieux **rem**.
- Les sélecteurs oui mais pas trop quand même. [MSIE 4095 Selector limit -- lol](http://www.habdas.org/msie-4095-selector-limit/)

> Une lecture sur les unités en CSS [Which CSS Measurements to use when](http://demosthenes.info/blog/775/Which-CSS-Measurements-To-Use-When)

## 5. Ecriture des classes

Afin d'utiliser au maximum la cascade nous utiliserons des classes avec héritages. Ou alors une technique un peu plus Ninja mais, bien plus légère et efficace ( *et aussi spécifique qu'une classe !* ).

```css
/***********************
*
*   Box Home page
*
************************/
.informations {width: 600px; margin: 0 auto}

.box {
    padding: 5px 10px;
    margin: 5px;
    border: 1px solid #eee;
    color: #777
}

.warn {color: red; border-color: pink}
.box.warn {border-color: red}
```

On a alors un dom qui se présente ainsi :

```html
<div class="informations">
    <div class="box"></div>
    <div class="box warn"></div>
    <div class="box"></div>
</div>
```

Ici `div.box.warn` est avec une couleur de police rouge et une bordure rouge également.

- Une classe est toujours en minuscule et peut contenir un séparateur, un tiret
- Si un id est utilisé pour le style ( *SSI vous maîtrisez le contexte* ) ne pas le sur-classifier div#kikoo est inutile.
- Pas plus de 4 classes max pour un tag
- Pas besoin de faire des selecteurs profonds, plus il est simple plus on passe dessus vite. ex : `.table-responsive>.table-bordered>thead>tr>th:first-child` cf la source de Twitter Bootstrap.

> Un article à propos de la sur-classification des CSS [Don’t Over-Specify Your CSS Code](http://robertnyman.com/2007/10/18/dont-over-specify-your-css-code/)

### Mode avancée

Si vous êtes à l'aise avec vos CSS vous pouvez passer du côté obscur de l'intégrateur, la manipulation d'attribut. Si vous n'êtes pas vraiment à l'aise utilisez ce guide : [The Skinny on CSS Attribute Selectors](http://css-tricks.com/attribute-selectors/).

Par exemple ici la classe `.box` n'est pas forcément nécessaire, nous pouvons aller beaucoup plus loin en conservant un bon niveau de lisibilité.

```css
[class^="box-"] {
    padding: 5px 10px;
    margin: 5px;
    border: 1px solid #eee;
    color: #777
}
.box-error {color: red}
.box-success {color: green}
.box-warn {color: orange}
```
On a alors un dom qui se présente ainsi :

```html
<div class="informations">
    <div class="box-success"></div>
    <div class="box-error"></div>
    <div class="box-warn"></div>
</div>
```

- div.box-success à une couleur verte
- div.box-error à une couleur rouge
- div.box-warn à une couleur orange

#### Qu'est-ce que cela apporte ?

Le but est de réduire la complexité du CSS. Par contre, cela impose de lire aisément les CSS et d'avoir pas mal d'expérience. Mais, ensuite on a un contexte plus explicite, donc ce n'est que du bonheur.

Le code est tout aussi verbeux et générique. On ne gagne pas là-dessus. Dans le dom on gagne une classe, cool ( *osef* ), par contre on a un contexte bien plus expressif pour la personne qui ne comprend pas très bien son CSS ( *dafuq la logique* ).

Exemple qui tourne en ce moment :

```css
[class^="kaction-"] {
    display: inline-block;
    width: 15px;
    height: 15px;
    border: 0;
    background-color: transparent;
    background-repeat: no-repeat;
    vertical-align: top;
    text-indent: -9999px
}

.kaction-edit {background-image: url(/static/images/picto/edit.png)}
.kaction-delete {background-image: url(/static/images/picto/bin.png)}
.kaction-duplicate {background-image: url(/static/images/picto/duplicate.png)}
.kaction-password {background-image: url(/static/images/picto/password.png)}
```

On a ici un exemple de boutons qui sont simple à enrichir, pour tous.

### Mauvais nomage

```css
.h {}
.h__toto_truc {}
.h-b {}
```

Est-ce que tu arrives à comprendre ce que c'est ? Moi non plus.

```css
.font-size-12 {}
.m20 {}
.p10 {}
```

Non, car le **CSS Atomique** c'est exactement pareil que de faire ça : `style="font:12px; margin:20px;padding:10px"`. En gros, ce n'est pas du CSS.

Alors, oui c'est plus simple on cale ça partout. Comme une balise style inline hein. C'est juste moins important donc on peut aisément passer dessus. Moi je n'aime pas.

> Petite anecdote, au travail l'autre jour un front, venu tout droit deJava ( *le pauvre* ) a eu exactement la même réflexion que moi. Comme quoi...


## 6. Préprocesseurs ?

Les préprocesseurs c'est bien très bien. Mais ceux-ci imposent certaines choses :
- Connaitre les CSS pour ne pas produire une CSS en carton
- Avoir un langage différent ( *mais qui permet de faire des choses ultra puissantes* )
- Compiler sa CSS
- Un debug un peu moins sympa
- Pour ceux qui ne s'en servent pas, entendre dans 80% des cas des arguments de front ne sachant pas ce qu'est le CSS, donc des arguments de merde.

Je ne suis pas contre, mais ici on parle de CSS.
Bilan : non.

> Si tu veux te lancer quand même car tu te touches en CSS, pars vers Sass. Puis pour trouver de l'information et un frenchie qui se touche bien avec Sass va voir [Hugo Giraudel](http://hugogiraudel.com)

## 7. Le futur

Et si on expérimentait Flexbox ? Voir les performances sur Android et iOS serait sympathique. On pourrait aussi voir son influence sur les FPS.

[A Complete Guide to Flexbox](http://css-tricks.com/snippets/css/a-guide-to-flexbox/)

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
- [Emmet LiveStyle](http://livestyle.emmet.io/) Pour éditer son CSS dans Sublime Text et rafraichir uniquement le CSS dans le navigateur ( *pas de refresh* ). Ou écrire du devtools dans ST2.
- [Flexy boxes](http://the-echoplex.net/flexyboxes/) Pour les flexbox
- [CSSCSS](http://zmoazeni.github.io/csscss/) Pour voir la redondance au sein de votre CSS
- [Em Baseline Generator](http://joshnh.com/tools/em-baseline-generator.html) Car l'em c'est bon pour la santé.
- [CSS Almanac](http://css-tricks.com/almanac/) Pour comprendre ce que sont les sélecteurs CSS et qui sont-ils. Idem pour les propriétés.
- [What CSS to prefix?](http://shouldiprefix.com/) Can I use version user-friendly
- [CSS Compatibility and Internet Explorer](http://msdn.microsoft.com/en-us/library/cc351024.aspx) un classique à garder

## 9. Remerciements

A vous :)
