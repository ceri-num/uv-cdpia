# Finalisation de l'ontologie

Dans cette section, nous allons finaliser notre ontologie : couverture, propriétés complexes, etc. Toutes ces étapes qui ne sont pas "directes" lorsqu'on réalise l'alignement avec les propriétés.

## Fermons notre margarita !

Comme précisé dans l'[étape 3](step3.md), OWL spécule en monde ouvert, autrement dit ce qui n'est pas défini peut peut être exister quand même. Or, si on regarde attentivement la garniture de notre margarita, on remarque qu'elle est compléte et finale : une margarita n'a pas d'autres éléments !

Aussi, on va fermer \(ou figer\) le concept de margarita à sa définition actuelle. Pour ce faire :

1. Retournez sur l'onglet `Entities > Classes`
2. Cliquez sur `Marguerita_pizza`
3. Dans la zone de description \(normalement en bas à droite\), sélectionnez une des lignes qui contient une propriété `has_topping` en cliquant dans sa case
4. Faites un click droit, puis sélectionnez `Create closure axiom`. Cela va vous créer une nouvelle propriété restrictive sur votre margarita. Il s'agit d'une union des deux garnitures
5. \(Optionnel\) vous pouvez éditer cette relation et la définir comme l'intersection des deux garnitures en remplaçant `or` par `and`.

## Définir des classes par leurs contraintes

Dans l'étape précédente, nous avons intentionnellement laissé la pizza `Spicy_beef_pizza` sans garniture. En réalité, il est souvent plus commode de décrire un ensemble de restrictions qui, une fois agrégées et convertis en classe, vont véhiculer une sémantique qui est celle de la classe que l'on veut représenter. C'est ce qu'on va faire ici.

1. Créer une sous classe de `Pizza_topping` que l'on nommera `Spicy_topping`
2. Dans la zone de description, rajouter la contrainte de super classe `has_spiciness some Hot_value` dans le champ `subclassOf`. On dit littéralement que `Spicy_topping` est à la fois une sous classe et est très forte.
3. Faîtes un click droit sur `Spicy_topping`, et sélectionnez `Convert to defined class`. Cela créer une seule expression qui combine \(créer l'intersection\) de vos deux contraintes précédentes \(`Pizza` et `has_spiciness some Hot_value`\).
4. Sélectionnez votre `Hot_and_spicy_pizza`
5. Ajouter une contrainte de super classe `has_topping some Spicy_topping` dans le champ `subclassOf` de la zone de description.
6. Convertissez cette classe en classe définie \(cf. 3.\)

{% hint style="info" %}
Vous n'arrivez pas à créer une nouvelle contrainte de type `has_spiciness some Hot_value` ? Dans ce cas, choisissez d'abord une classe à rajouter \(par exemple `Hot_value`\) puis modifiez là et aller dans le `Class expression editor` et rajouter manuellement le début de la règle avec la classe : `has_spiciness some`.
{% endhint %}

Voila, notre pizza hot & spicy se définit comme étant une pizza qui a une garniture épicée, et le concept de garniture épicée est définit comme ayant une valeur forte ! La boucle est bouclée !

## Des concepts plus riches

On va enfin voir comment créer des concepts beaucoup plus avancés que simplement une seule règle.

### La cheesy

Pour considérer une pizza comme étant une pizza fromage, on va partir du principe qu'il faut au moins deux fromages différents dessus, sinon il s'agit d'une vulgaire pizza.

Pour exprimer cette nouvelle contrainte, il faut repérer quels éléments elle implique. Si on regarde attentivement :

* Une cardinalité : ici **2**
* Un opérateur : ici **minimum**
* ce qu'on met dessus : ici **`Cheese_topping`**
* la relation : ici **`has_topping`**

Si on assemble tous nos morceaux, ça nous donne : `has_topping min 2 Cheese_topping`.

Maintenant, pour dire que notre `Cheesy_pizza` doit respecter cette contrainte \(et que c'est toujours une pizza\), il faut modifier la clause `Pizza` dans la ligne `SubClassOf` dans la zone de description pour faire apparaître l'intersection de ces deux éléments. Vous devez donc écrire :

```text
Pizza and has_topping min 2 Cheese_topping
```

### La vegan

Contrairement à ce qu'on pourrait croire, une pizza vegan, ce n'est pas que simplement de la pâte ! Il s'agit d'exclure tous les éléments de provenance animal, sans distinction. Aussi, il ne faut pas qu'il y ait sur notre pizza vegan de viande, de poisson **ni** de fromage !

Astuce syntaxique, puisque l'on utilise des **ni**, il s'agit de l'union des éléments que l'on cite dans le texte. Ici donc `viande or poisson or fromage`. Aussi pour parler de ces trois garnitures, on a : `has_topping some (Meat_topping or Fish_topping or Cheese_topping)`.

Pour dire que l'on en veut pas, on prend simplement l'inverse de l'ensemble que l'on vient de créer, à savoir `not(X)`.

En combinant nos morceaux, la définition de notre pizza vegan s'écrit donc :

```text
Pizza and not(has_topping some (Meat_topping or Fish_topping or Cheese_topping))
```

Et voila, on peut y mettre des fruits et des légumes en sommes !

{% hint style="info" %}
On aurait donc aussi pu l'écrire `has_topping only (Fruit_topping or Vegetable_topping)` !
{% endhint %}

## Qu'est-ce qu'on vient de faire ?

Dans cette section, on a vu comment créer des classes à partir d'expressions plus complexe.

On a également vu comment exploiter les notions d'ensemble pour construire les classes \(disjonction, conjonction, etc.\).

