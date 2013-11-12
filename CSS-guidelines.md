# Pour une conception simple et cohérente de vos intégrations

Ce document a pur but de définir une liste de recommendations pour permettre une intégration simple et compréhensible.

Ce document est destiné avant tout à servir au sein de mon équipe dans mon travail. Ce n'est pas gravé dans le marbre, sauf pour les personnes travaillant directement avoir moi sur de l'intégration.

Merci de bien vouloir contribuer.
Exprimez vos idées, vos intérogations et vos remarques en bien ou en mal.


## Introduction

Une intégration n'est pas facile. Partir ainsi est le meilleur moyen de passer à coté de son intégration. Celle-ci doit facilement pouvoir évoluer et pouvoir et changer de mains, sans pour autant  perdre le dev ou l'intégrateur.

Le mot d'ordre est [KISS](http://wikipedia.org/KISS) issu du monde unix. Puis au passage DRY aussi.

Et ne pas oublier que dans CSS il y a cascade.

- On ne doit pas se demander combien d'intégrateurs/dev sont passés sur une intégration
- Si vous ne savez pas comment faire, c'est qu'il faut relire ce document
- Si vous ne savez toujours pas, suivez les conventions pour adapter le problème

## Table des matières

1. [Indentation](#1-indentation--)
2. [Commentaires](#2-commentaires--)
3. [Formatage](#-formatage--)
4. [Quelques éléments indispensable](#chaptire4)
5. [Ecriture des classes](#chaptire5)
6. [Préprocesseurs ?](#chaptire6)
7. [Le futur](#chaptire7)

## Avant de commencer

- **Ne jamais styliser sur un id**
- **Ne jamais utliser !important**
- Ne jamais mettre une seule typo dans une font-family
- Le moins possible de classes magiques (.left {float: left;})
- Lire et imprimer ca :  [Learn CSS Specifishity with plankton, fish and sharks](http://www.standardista.com/wp-content/uploads/2012/01/specifishity1.pdf)

### Pourquoi ID et !important

Styliser avec ID n'est pas un mal en soi, c'est juste que l'id étant unique ce style est "mort"pour la suite. On ne peut le replacer l'extendre. Cela dit sur certains contextes on peut très bien s'en servir. Il suffit de maitriser le contexte.


## 1. Indentation  <span id="chaptire1"></span>

Les espaces, ceux-ci au nombre de 4. C'est aéré et plus lisible. Puis l'espace passe parfaitement partout ce qui n'est pas le cas de la tabulation.

- **On ne mélange pas les deux**

> Pensez à configurer votre éditeur comme SublimeText pour qu'il enregistre vos fichiers avec des espaces automatiquement.


## 2. Commentaires  <span id="chaptire2"></span>

Comme partout un code sans commentaires c'est de la merde. Personne ne possède la même logique et compréhension du code. Donc on commente sans discuter.

Sauf que nous faisons du CSS, donc nos classes sont **expressives** et donc il suffit de mettre un bloc de code au dessus de `.header` par exemple pour toutes les modifications relatives à ce qui est dedans. Ce sont des commentaires de zone/section.

```css
/***********************
*
*    Header
*
************************/
.header::before {
	content: '42'
}
```

On ne met pas d'étoile en fin, c'est de la perte de temps pour juste de l'ésthétique, qui de plus est lors du dev.

Sinon en plein millieu de votre code, un commentaire classique suffit :

```css
.post-content {
	padding: 2px 4px;

	/* Un peu de magie */
	margin-left: 13,37px

	border-color: #BADA55
}
```

Le fait de sauter une ligne avant et après met en valeur ce commentaire.

## 3. Formatage  <span id="chaptire3"></span>

- Un espace entre le nom du tag/sélécteur et l'accolade ouvrante
- Retour à la ligne après chaques propriétées
- Pas de point virgule pour la dernière propriété
- Toujours des doubles guillements pour les sélécteurs d'attrubuts
- Indentation de 4 espaces avant chaque propriétée
- Pas d'espace entre la propriété et le :
- Un espace après le :
- Pas d'inline si > 2 propriétées
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

-1 Le display
-2 La taille
-3 Les modifications tailles
-4 Les background/couleurs
-5 La typo

Après c'est une recommendation, on peut faire avec un ordre alphabéthique. Cela dit on va tenter d'automatiser par la suite un parsing du CSS pour trier tout ce code proprement.
> Une piste [The Greatest tool for sorting CSS properties in specific order](http://csscomb.com/) ou alors un truc avec Grunt.

## 4. Quelques éléments indispensable  <span id="chaptire4"></span>

- `[type=submit]` = non préférez une structure propre : `[type="submit"]`
- `border:0px` = non l'unité est inutile ici -> `border: 0`
- `-webkit-border-radius` **Non** [What CSS to prefix?](http://shouldiprefix.com/)
- `box-sizing: border-box` Amen. L'utilsier tu dois, pourquoi ? [box-sizing, et pourquoi pas ?](http://blog.goetter.fr/post/27612618411/box-sizing-et-pourquoi-pas)
- Pas de tailles dans line-height cf [Line-Height Units](http://tzi.fr/CSS/Text/line-height-units)
- Le PX m'a tuer. Préférons **em** ou mieux **rem**.

> Une lecture sur les unités en CSS [Which CSS Measurements to use when](http://demosthenes.info/blog/775/Which-CSS-Measurements-To-Use-When)

## 5. Ecriture des classes  <span id="chaptire5"></span>

Afin d'utiliser au maximum la cascade nous utiliserons des classes avec héritages.

Par exemple souhaite styliser nos box sur une home page, celles-ci se ressemble, mais pas trop.

```css
/***********************
*
*	Box Home page
*
************************/
.box-info {width: 600px; margin: 0 auto}

.box {
	padding: 5px 10px;
	margin: 5px;
	border: 1px solid #eee;
	color: #777
}

.box.warn {color: red}
```

On a alors un dom qui se présente ainsi :

```html
<div class="box-info">
	<div class="box"></div>
	<div class="box warn"></div>
	<div class="box"></div>
</div>
```

- Une classe est toujours en minuscule et peut contenir un separateur, un tiret
- Si un id est utilisé pour le style (SSI vous maitrisez le contexte) ne pas le sur classifier div#kikoo est inutile.
- Idem pour une classe, on peut surclassifié cette dernière mais pas inutilement SVP
- On fait des classes modulables qui peuvent se chainer
- Pas plus de 4 classes max pour un tag
- On chaine si on a un traitement specifique pour cette classe extend d'une autre
- Pas besoin de faire des selecteurs profond, plus il est simple plus on passe dessus vite.

### Mode avancée

Si vous êtes à l'aise avec vos CSS vous pouvez passer du côté obscur de l'intégrateur, la manipulation d'attribut.

Par exemple ici la classe `.box` n'est pas forcément nécessaire, nous pouvons aller beaucoup plus loin en concervant un bon niveau de lisibilitée.

```css
[clas^="box-"] {
    padding: 5px 10px;
	margin: 5px;
	border: 1px solid #eee;
	color: #777
}
.box-warn {color: red}
```


On a alors un dom qui se présente ainsi :

```html
<div class="box-info">
	<div class="box-success"></div>
	<div class="box-error"></div>
	<div class="box-warn"></div>
</div>
```

#### Qu'est ce que ca apporte ?

Le but est de réduire la complexité du CSS, cela dit ca impose d'en avoir une excellente compréhension. Mais ensuite on contextualise plus nos css.

Le code est tout aussi verbeux et générique. On ne gagne pas là dessus dans le dom, par contre on a un contexte bien plus expressif pour la personne qui ne comprend pas très bien son CSS.

Par contre en contrepartie on peut se retrouver avec des classes fantômes, sauf si on fait par exemple : `[clas^="box-"].box`. De la redondance au service de la clarté.

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

Est ce que tu comprends ce que c'est ? Moi non plus.

```css
.font-size-12 {}
.m20 {}
.p10 {}
```

Non car le **CSS Atomique** c'est exactement pareil que de faire ca : `style="font:12px; margin:20px;padding:10px"`. En gros, ce n'est pas du CSS.


## 6. Préprocesseurs ?  <span id="chaptire6"></span>

Les préprocesseurs c'est bien très bien. Sauf que si vous les utilisez sans connaitre le CSS vous perdez votre temps. Car bien utilisé ca produit de belles choses, sinon non, bien au contraire.

Bilan : non.
Sinon SASS.

## 7. Le futur  <span id="chaptire7"></span>

Et si on expérimentait Flexbox ? Voir les performances sur Android et iOS serait sympathique. On pourrait aussi voir son influence sur les FPS.

[A Complete Guide to Flexbox](http://css-tricks.com/snippets/css/a-guide-to-flexbox/)

