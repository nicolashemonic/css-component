Css-Component
=============

Méthodologie CSS pour la conception de composants graphiques autonomes, configurables et réutilisables.

## Définition

Un composant graphique est un élément de base d'une interface graphique avec lequel l'utilisateur peut éventuellement interagir (par exemple une liste, un menu, etc). L'assemblage de plusieurs composants forme une interface graphique complète.

## Principe général

1. [Composant autonome](#composant-autonome)
2. [Créer plutôt que modifier](#creer-plutot-que-modifier)
3. [Dépendance au DOM](#dependance-au-dom)
4. [Faible encapsulation](#faible-encapsulation)
5. [Documentation](#documentation)

<a name="composant-autonome"></a>
### Composant autonome

Chaque composant est autonome. Il possède son propre HTML, CSS, JavaScript ou tout autre ressource limitant toute dépendance au contexte d'affichage dans lequel il évolue. Idéalement, le CSS et le JavaScript sont écrits dans des fichiers qui leurs sont propre afin de les extraire facilement du contexte dans lequel ils sont ancrés.

<a name="creer-vaut-mieux-que-modifier"></a>
### Créer plutôt que modifier

Un composant répond à un besoin qui lui est propre. Il est conseillé de limiter sa modification au sein d'un contexte.

Si le besoin est trop éloigné de sa conception originale il est préférable d'en créer un nouveau pour répondre plus précisément au nouveau besoin.

Une variation ne devrait pas modifier radicalement l'apparence du composant ou demander à l'utilisateur de comprendre comment il fonctionne.

<a name="dependance-au-dom"></a>
### Dépendance au DOM

De manière générale, le style appliqué à un élément HTML doit correspondre à une classe. 

Il est important de ne pas appliquer de style à un élément particulier du DOM ou à une structure particulière du DOM.
Cela limite très fortement la dépendance à la structure HTML et améliore grandement la robustesse de l'intégration tout en facilitant la lecture du CSS.

<a name="faible-encapsulation"></a>
### Faible encapsulation

La compléxité est un problème important pour les grosses applications évolutives. Moins les composants sont imbriqués et plus l'application en récolte les bénéfices.

Tout d'abord, limiter au maximum la réutilisation de code à travers les composants. Il est préférable d'isoler chaque composant plutot que d'essayer de limiter la répétition de ses propriétés en les mutualisant. Ceci aurait pour incidence de rendre des composants dépendants entre eux.

Un composant ne devrait pas avoir connaissance de l'éxistance ou de l'apparence d'un composant qui lui est imbriqué. Il est préférable de considérer dans ce cas que le composant imbriqué fait partie intégrante du composant et qu'il doit en avoir sa propre implémentation.

<a name="documentation"></a>
### Documentation

Ecrire de petits composants indépendants bien documenté.
La documentation précise comment le composant devrait être utilisé, pourquoi certaines propriétés CSS sont nécéssaires lors de son implémentation. Il est important de ne pas considérer que le CSS est une documentation en soit.

## Convention de nommage

L'écriture du CSS se fait en dash-case, tout en minuscule.

Un composant est constitué de la manière suivante :

1. [Composant](#composant)
2. [Variation](#variation)
3. [Descendant](#descendant)
4. [Qualifieur](#qualifieur)

<a name="composant"></a>
### Composant

La classe d'un composant commence toujours par le mot clé `this` qui permet de l'identifier facilement et d'en délimiter sa porté.

Son nom est l'élément central de toute sa structure :  
`this-<component-name>[--variation-name|-descendent-name]`

Cette convention comporte plusieurs bénéfices pour la lecture et l'écriture du HTML et du CSS:

* Aide à distinguer les classes de base du composant, de ses variations et de ses descendants
* Diminue considérablement la dépendance entre le DOM et le CSS
* Le poids du sélecteur reste faible (surcharge aisée)

```css
.this-component-name { }
```

```html
<div class="this-component-name"></div>
```

<a name="variation"></a>
### Variation

La classe d'une variation d'un composant commence par le nom de celui-ci séparé par deux tirets :  
`component-name--<variation-name>`

Elle permet de décliner l'affichage du composant sous différents styles. La classe doit être ajouté à l'élément HTML en plus de la classe du composant.

```css
.component-name--variation-name { }
```

```html
<div class="this-component-name component-name--variation-name"></div>
```

<a name="descendant"></a>
### Descendant

La classe d'un descendant d'un composant commence toujours par le nom de celui-ci :  
`component-name-<descendent-name>`

La classe est attachée à un noeud du composant, celle-ci applique un style directement sur l'élément HTML sur lequel elle est ajoutée.

```css
.component-name-descendent-name { }
```

```html
<div class="this-component-name component-name--variation-name">
  <p class="component-name-descendent-name"></p>
</div>
```

<a name="qualifieur"></a>
### Qualifieur

La classe d'un qualifieur attachée à un composant commence toujours par le mot clé `is` :  
`is-<qualifier-name>`

Elle peut être utilisée pour qualifier une apparence (couleur, typo, etc) ou/et un état (ouvert - fermé, affiché - masqué, etc).

Il est interdit de styler cette classe directement, elle doit être utilisée conjointement avec une classe du composant.

A noter qu'une classe qualifieur peut être ajoutée ou supprimée par le JavaScript pour modifier l'état du composant à un instant _t_.

```css
.component-name-descendent-name.is-qualifier-name { }
```

```html
<div class="this-component-name component-name--variation-name">
  <p class="component-name-descendent-name is-qualifier-name"></p>
</div>
```


