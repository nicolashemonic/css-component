structural-css
==============

Méthodologie CSS de conception de composants graphiques réutilisables et configurables.

L'objectif est d'apporter une convention à l'écriture du CSS en intégrant des composants graphiques simples et autonomes conçus pour le templating côté client.

## Principe général

1. [Composant autonome](#composant-autonome)
2. [Créer plutôt que modifier](#creer-plutot-que-modifier)
3. [Dépendance au DOM](#dependance-au-dom)
4. [Faible encapsulation](#faible-encapsulation)
5. [Documentation](#documentation)

<a name="composant-autonome"></a>
### Composant autonome

Chaque composant est autonome. Il possède son propre HTML, CSS, JavaScript ou tout autre ressource limitant toute dépendance au contexte d'affichage dans lequel il évolue.

Le bénéfice est de pouvoir le réutiliser facilement.

<a name="creer-vaut-mieux-que-modifier"></a>
### Créer plutôt que modifier

Un composant répond à un besoin qui lui est propre. Il est conseillé de limiter sa modification au sein d'un contexte.

Si le besoin est trop éloigné sa conception originale il est préférable d'en créer un nouveau pour répondre plus précisément au nouveau besoin.

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

L'écriture se fait en dash-case tout en minuscule.

1. [Composant](#composant)
2. [Variation](#variation)
3. [Déscendant](#descendant)
4. [Qualifieur](#qualifier)

<a name="composant"></a>
### Composant

Sa classe commence toujours par le mot clé `this` ce qui permet de l'identifier facilement et d'en délimiter sa porté.

Son nom est l'élément central de toute sa structure:
`this-<component-name>[--variation-name|-descendent-name]`

Cette convention comporte plusieurs bénéfices pour la lecture et l'écriture du HTML et CSS:

* Aide à distinguer les classes de base du composant, de ses variations et de ses déscendants
* Diminue considérablement la dépendance entre le DOM et le CSS
* Le poids du sélecteur reste faible

```css
.this-component-name { }
```

```html
<div class="this-component-name"></div>
```

<a name="variation"></a>
### Variation

Une variation d'un composant est une classe qui modifie l'affichage de base du composant sous différentes formes. La classe doit être ajouté à l'élément HTML en plus de la classe du composant.

```css
.component-name--variation-name { }
```

```html
<div class="this-component-name component-name--variation-name"></div>
```

<a name="descendant"></a>
### Déscendant

Un déscendant est une classe attachée à un noeud du composant. Cette classe applique un style directement sur l'élément HTML sur lequel elle est ajoutée.

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

Une classe qualifieur commence toujours par le mot clé `is`:
`is-<qualifier-name>`

Elle peut être utilisée pour qualifier une apparence (couleur, typo, etc) ou/et un état (ouvert - fermé).

Il est important de noter qu'il est interdit de styler cette classe directement, elle doit être utilisé conjointement avec une classe.

A noter qu'une classe qualifieur peut être ajouté ou supprimé par le JavaScript pour modifier l'état du composant à un instant t.

```css
.component-name-descendent-name.is-qualifier-name { }
```

```html
<div class="this-component-name component-name--variation-name">
  <p class="component-name-descendent-name is-qualifier-name"></p>
</div>
```


