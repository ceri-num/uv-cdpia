# Approximation sémantique

## Introduction

Introduire de la sémantique dans les données ne sert pas qu'à faire joli, surtout dans le cas des graphes conceptuels et des ontologies.

Dans des bases de connaissances taxonimiques par exemple (*e.g.* GC et ontologie), il devient possible d'exploiter la proximité sémantique des termes (classes) et des relations décrites pour étendre le raisonnement et chercher de l'information et des solutions.

{% hint style="success" %}
Ce type de raisonnement permet de produire des résultats non-exacts ; pratique par exemple lors d'une recherche et que l'on ne trouve pas de résultat pour la requête utilisateur ! C'est par exemple ce qui est effectué dans mes travaux [[Lebis19]](../REF.md/#lebis19).
{% endhint %}

## Distance sémantique

À partir d'une ontologie, il est possible de définir des **métriques** et des **caractéristiques** dépendantes de la position des classes de l'ontologie les uns par rapport aux autres, en fonction des relations qu'ils partagent. Cela permet notamment :

* De dériver **approximativement** le type et les propriétés d'une classe qu'on insère dans la base de connaissance et dont on a aucun connaissance *a priori* ;
* De **supposer** d'inconsistences et de propriétés ;
* D'étendre l'espace de recherche.

![Illustration d'une approximation sémantique basée sur la taxonomie, [Lebis19].](assets/approx_sem_by_distance.png)

On peut envisager plusieurs approximations sémantiques qui ont un sens, comme celle taxonimique par exemple.

### Profondeur taxonimique

Cette approximation se fonde sur le fait que si `B est subsumé par A` (*i.e.* `B` est un `A`), alors `B` partage des propriétés intrinsèques avec `A`. Aussi, `A` peut être un candidat potentiel lors de recherche, bien que moins précis que si ça avait été B.

{% hint style="info" %}
Cette taxonomie s'établit naturellement dans une ontologie en utilisant les notions de `subclassOf`,  comme dans :`Chien subclassOf Mammifère`.
{% endhint %}

L'avantage de cette approche est que l'on peut remonter la chaîne prototypal d'un terme ; théoriquement, plus on s'éloigne de l'élément de référence, moins l'alignement est convenable et plus les incohérences sont présentes.

### Largeur taxonimique

À l'instar du parcours vertical du graphe ontologique des entités, on peut aussi imaginer un parcours horizontal des classes sous des termes parents, pour permettre la recherche de termes similaires à ceux initiaux.

### Largeur synonymique

À l'instar du parcours en largeur taxonimique du graphe ontologique des entités, on peut envisager un parcours en largeur basé sur la notion de synonymie.

Certains termes de l'ontologie se voient attribuer des relations de synonymies, ce qui nous permet d'aller explorer certaines autres parties du graphes jusqu'alors inaccessible.

*Exemple :*
> Si dans l'ontologie, on ajoute un concept où l'on a très peu de connaissance experte *a priori* - ici disons le concept de `Tesseract`. Tout ce que l'on sait, c'est qu'il s'agit d'un synonyme de `Cube Multi-dimensionnel` : on peut alors espérer dériver des informations de `Cube` lorsque l'on parlera de `Teseract`, sans pour autant en être sûr à 100%.

{% hint style="danger" %}
À l'inverse de la notion de parenté (*e.g.* `subclassOf`), la synonymie est un lien "artificielle" dans l'ontologie, représentable par une relation [symétrique](../ke/owl.md/#symetrique) entre deux éléments de l'ontologie (possédant éventuellement un degré).
{% endhint %}

## Métriques

Le but de quantifier l'approximation est d'indiquer le fait que, plus l'on s'éloigne de l'entité initiale, plus la pertinence de la relation risque de s'être dégradé ; aussi, lorsqu'on présente le résultat ou qu'on l'utilise, il faut savoir si l'on peut lui "faire confiance".

### Calcul

Dans la figure précédente, on calcule le score d'approximation *via* deux fonctions différentes qui s'établissent dans $$[0,1]$$ : une pour la profondeur, une pour la synonymie.

Classiquement, comme proposé dans [Corese06](../REF.md/#corese06), on peut définir la profondeur sémantique comme $$\frac{1}{(2^n)}$$ et la largeur comme $$\frac{1}{2}\times h$$. 

Pour les synonymes, cela dépendra de s'il s'agit de classes ou de relations. Un exemple de comment réaliser cela :

![Exemple de calcul de score d'approximation pour les relations d'une ontologie [Lebis19].](assets/approx_sem_score_rel.png)

### Modificateur sémantique

L'avantage de travailler dans un espace sémantique est la possibilité d'introduire des modificateurs pour moduler l'importance des similitudes, notamment concernant les synonymes - ce qui fait écho à la [logique flou](../ke/fzl.md).

On peut par exemple dire que `X` est un synonyme fort de `Y`, mais qu'il recouvre partiellement la notion véhiculée par `Z`. Ainsi, si lors d'une recherche ou d'un raisonnement, on est plus ou moins stricte sur la synonymie, l'on prendra ou ne prendra pas en compte `Z` comme résultat (et ce qu'il implique).

## Explicabilité

L'un des points forts des systèmes sémantiques et des systèmes experts est leur propension à pouvoir "expliquer" le raisonnement effectué (*i.e.* qu'elles règles ils ont suivis, comment leur base de faits s'est accrue...).

En exploitant ces principes, il devient également possible de fournir à l'utilisateur de l'information expliquant l'approximation sémantique, et surtout modérer la confiance qu'il doit accorder aux résultats en fonctions des "libertés" prises par le raisonneur.

Dans la figure ci-dessous, le système indique à l'utilisateur quel(s) éléments ont été respectés dans sa requête, et le score de confiance du résultat vis-à-vis de l'attente utilisateur (plus il est haut, mieux c'est).

![Capture d'écran de résultat d'une recherche basée sur l'approximation sémantique [Lebis19].](assets/approx_sem_coverage.png)