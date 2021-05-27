# Ontologie

## Introduction

{% hint style="info" %}
Soyez attentif, on pratiquera sur les ontologies dans la section de [Mise en pratique](../handson/tuto.md).
{% endhint %}

bla

Les étapes classiques pour l'élaboration d'une ontologie, d'après [Powell, 2015](../REF.md/#powell2015) :

1. Identifier votre **taxonomie** -- quels sont les éléments, les sous-éléments...
2. Quels éléments **non pas de relation** avec d'autres ?
3. Quels éléments "**héritent**" (*i.e.* sont des) de plusieurs éléments ?
4. Quels sont les **caractéristiques uniques** définissant un individu ?
5. Quels sont les **caractéristiques mesurables** d'un élément ?
6. Quels éléments sont **décrit par** l'entremise d'**autres éléments** ?

## Entités, relations

## A-BOX vs T-BOX

### Assertion component

```rdf
A est un B
```

```rdf
Bob est un Homme
```

### Terminological component

Tous les Étudiants sont des Personnes

Il y a deux types de personnes : des XX (Femme) et des XY (Homme).


## Propriétés des relations

Un propriété, appliquée à une relation, la conditionne et lui induit des contraintes supplémentaires qui seront utilisées lors du raisonnement.

Ce n'est pas obligatoire d'attribuer à une relation une propriété, mais cela peut aider à renforcer les contraintes d'intégrité du système que vous êtes en train de décrire.

Une relation peut donc avoir aucune, une ou plusieurs propriétés à la fois. Elles sont au nombres de 5 :

* Transitive (`owl;TransitiveProperty`)
* Symétrique (`owl;SymetricProperty`)
* Fonctionnelle (`owl;FunctionalProperty`) 
* Inverse de (`owl;inverseOf`)
* Fonctionnelle Inverse (`owl;InverseFunctionalProperty`)

{% hint style="info" %}
Les exemples qui suivent proviennent tous de la [documentation officielle](https://www.w3.org/TR/2004/REC-owl-guide-20040210/#PropertyCharacteristics) concernant le Web Ontology Language (OWL) de la W3C
{% endhint %}

### Transitive

Si une propriété $$P$$ est spécifiée comme **transitive**, alors $$\forall x, y, z$$ on a : $$P(x,y) \wedge P(y,z) \rightarrow P(x,z)$$.

Autrement dit, pour une même propriété, si il existe "un chemin de cette propriété" entre $$x$$ et $$z$$, alors cette propriété s'applique aussi entre $$x$$ et $$z$$.

*Exemple :*
> ```rdf
> <owl:ObjectProperty rdf:ID="locatedIn">
>   <rdf:type rdf:resource="&owl;TransitiveProperty" />
>   <rdfs:domain rdf:resource="&owl;Thing" />
>   <rdfs:range rdf:resource="#Region" />
> </owl:ObjectProperty>
> 
> <Region rdf:ID="SantaCruzMountainsRegion">
>   <locatedIn rdf:resource="#CaliforniaRegion" />
> </Region>
> 
> <Region rdf:ID="CaliforniaRegion">
>   <locatedIn rdf:resource="#USRegion" />
> </Region>
> ```
> Ici, on définit que la région `SantaCruzMountainsRegion` est `locatedIn` (située dans) la région `CaliforniaRegion`, et que cette dernière est `locatedIn` la `USRegion`. Puisque `locatedIn` est transitive, on peut **en déduire** que `SantaCruzMountainsRegion` est aussi `locatedIn` la `USRegion` !

### Symétrique

Si une propriété $$P$$ est spécifiée comme **symétrique**, alors $$\forall x, y$$ on a : $$P(x,y) \leftrightarrow P(y,x)$$.

Autrement dit, si une propriété est symétrique, elle est vraie ou fausse, qu'importe le sens des termes.

*Exemple :*
> ```rdf
> <owl:ObjectProperty rdf:ID="adjacentRegion">
>   <rdf:type rdf:resource="&owl;SymmetricProperty" />
>   <rdfs:domain rdf:resource="#Region" />
>   <rdfs:range rdf:resource="#Region" />
> </owl:ObjectProperty>
> 
> <Region rdf:ID="MendocinoRegion">
>   <locatedIn rdf:resource="#CaliforniaRegion" />
>   <adjacentRegion rdf:resource="#SonomaRegion" />
> </Region>
> ```
> Ici, on définit en plus de la relation `locatedIn` la relation `adjacentRegion`, qui à pour domaine une `Region` et une portée de `Region`. La région `MendocinoRegion` est définie comme adjacente à la région `SonomaRegion`. On peut donc **en déduire** que `SonomaRegion` est aussi adjacente à `MendocinoRegion`. Par contre, il n'y a pas symétricité pour la relation `locatedIn CaliforniaRegion` concernant `SonomaRegion` : on n'a aucune information d'où elle est située.

### Fonctionnelle

Si une propriété $$P$$ est spécifiée comme fonctionnelle, alors $$\forall x, y, z$$ on a : $$P(x,y) \wedge P(y,z) \rightarrow y = z$$.

Autrement dit, si une propriété est fonctionnelle, le terme en portée est **"unique"**.

{% hint style="info" %}
Bien qu'on puisse dire que la portée est unique, cela n'empêche pas d'exprimer $$P(x,y)$$ et $$P(x,z)$$, au contraire. Si on sait que la `chocolatine` est une `viennoiserie`, mais pas le `petitPain`, que la fonction `mange` est fonctionnelle, et qu'on a un moment `mange(Bob,chocolatine)` puis plus tard `mange(Bob,petitPain)`, on en déduit que `chocolatine = petitPain` **ET** que `petitPain` est une `viennoiserie`. Pratique, en plus de mettre fin au conflit (on sait tous que la chocolatine est la vrai).
{% endhint %}

Exemple :

> ```rdf
> <owl:Class rdf:ID="VintageYear" />
> 
> <owl:ObjectProperty rdf:ID="hasVintageYear">
>   <rdf:type rdf:resource="&owl;FunctionalProperty" />
>   <rdfs:domain rdf:resource="#Vintage" />
>   <rdfs:range  rdf:resource="#VintageYear" />
> </owl:ObjectProperty>
> ```
> In our wine ontology, \texttt{hasVintageYear} is functional. A wine has a unique vintage year. That is, a given individual \texttt{Vintage} can only be associated with a single year using the \texttt{hasVintageYear} property. It is not a requirement of a \texttt{owl:FunctionalProperty} that all elements of the domain have values.

### Inverse de

```rdf
<owl:ObjectProperty rdf:ID="hasMaker">
  <rdf:type rdf:resource="&owl;FunctionalProperty" />
</owl:ObjectProperty>
  
<owl:ObjectProperty rdf:ID="producesWine">
  <owl:inverseOf rdf:resource="#hasMaker" />
</owl:ObjectProperty>
```

### Fonctionnelle Inverse

```rdf
<owl:ObjectProperty rdf:ID="hasMaker" />
  
<owl:ObjectProperty rdf:ID="producesWine">
  <rdf:type rdf:resource="&owl;InverseFunctionalProperty" />
  <owl:inverseOf rdf:resource="#hasMaker" />
</owl:ObjectProperty>                                     ¬ 
```

## Représentation des ontologies

RDF et rdfs

## Vers du web sémantique : Requêtage et "Endpoints"

