structural-css
==============

Méthodologie CSS de conception de composants graphiques réutilisables et configurables.

L'objectif est d'apporter une convention à l'écriture du CSS en intégrant des composants graphiques simples et autonomes conçus pour le templating côté client.

## Principe général

1. [Composant autonome](#composant-autonome)
2. [Etendre plutot que modifier](#etendre-plutot-que-modifier)
3. [Dépendance](#dependance)
4. [Faible encapsulation](#faible-encapsulation)
5. [Documentation](#documentation)

<a name="composant-autonome"></a>
## Composant autonome

Chaque composant est autonome. Il possède son propre HTML, CSS, JavaScript ou tout autre ressource limitant toute dépendance au contexte d'affichage dans lequel il évolue.

<a name="etendre-plutot-que-modifier"></a>
## Etendre plutot que modifier

Etendre l'affichage d'un composant avec une ou plusieurs classes est préféré à la modification directe des sélecteurs qui lui sont propre. Cette pratique limite la compléxité au sein du contexte.

Il est préférrable de limiter le nombre de variation d'un composant. Une variation ne devrait pas modifier radicalement l'apparence du composant ou demander à l'utilisateur de comprendre comment il fonctionne.

<a name="dependance"></a>
## Dépendance

De manière générale le style appliqué à un élément HTML doit correspondre à une classe. 
Il est important de ne pas appliquer le style à un élément particulier du DOM ou à une structure particulière du DOM.
Cela limite très fortement la dépendance à la structure HTML et facilite la lecture du CSS et la maintenabilité.

<a name="faible-encapsulation"></a>
## Faible encapsulation

La compléxité est un problème important pour les grosses applications. Moins les composants seront imbriqués et plus l'application en récoltera les bénéfices.

Tout d'abord, limiter au maximum la réutilisation de code à travers les composants. Il est préférable d'isoler chaque composant plutot que d'essayer de limiter la répétition des propriétés.

Les composants ne devrait pas avoir connaissance de l'éxistance ou de l'apparence des composants qui leur sont imbriqué. Il est préférable de considérer dans ce cas que le composant imbriqué est une partie intégrante du composant et qu'il doit en avoir sa propre implémentation.

<a name="documentation"></a>
## Documentation

Ecrire de petits composants indépendants bien documenté.
La documentation précise comment le composant devrait être utilisé, pourquoi certaines propriétés CSS sont nécéssaires lors de son implémentation. Il est important de ne pas considérer que le CSS est une documentation en soit.

## Syntaxe d'un composant graphique

* Ecriture en dash-case
* Le nom commence par le mot clé `this`

```css
.this-component-name { }
.component-name--variation-name { }
.component-name-descendant { }
.is-qualifier-name { }
```
