# Ontologie

## Introduction

{% hint style="info" %}
Soyez attentif, on pratiquera sur les ontologies dans la section de [Mise en pratique](../handson/tuto.md).
{% endhint %}

L'ontologie, quelque soit le contexte dans lequel on la considère est un concept complexe à assimiler. On retrouve initialement le concept d'ontologie en philosophie, qui se définit comme :

> Partie de la philosophie qui a pour objet l'étude des propriétés les plus générales de l'être, telles que l'existence, la possibilité, la durée, le devenir. [[CNRTL]](https://www.cnrtl.fr/lexicographie/ontologie)

En informatique, la notion d'ontologie change quelque peut. Elle conserve sont caractère descriptif afin de capter les interrelations qui existent au sein d'une sous-partie d'un monde observé ; mais elle introduit surtout une notion forte de modélisation des éléments qui constituent ces interrelations : les "objets" et les "relations" qu'ils ont.

{% hint style="success" %}
En un sens, une ontologie est un framework conceptuel d'un domaine précis, permettant de modéliser les éléments du discours, leurs relations et leurs caractéristiques sous la forme d'un graphe $$\mathcal{G}=(V,E)$$ où $$V$$ sont les éléments, et $$E$$ les relations.
{% endhint %}

La particularité d'une ontologie est qu'elle est bien plus qu'une simple taxonomie ; elle l'est d'une part : c'est un graphe qui décrit la hiérarchie des concepts (éléments **et** relations) impliqués. Ainsi, les concepts qui interviennent en bas de la taxonomie "héritent" des propriétés de leurs ancêtres.

Mais c'est également une taxonomie enrichie de relations logiques complexes qui interviennent entre les éléments du discours, comme l'appartenance à des groupes d'éléments, la symétrie d'une relation, l'exclusivité d'une relation et plein d'autres éléments.

{% hint style="info" %}
On peut en effet faire de l'"héritage" sur les relations également ! Par exemple dire que `hasVeryGoodFriend(x,y)` "hérite" de `hasFriend(x,y)`.
{% endhint %}

{% hint style="warning" %}
On ne parle pas d'héritage, mais de subsomption ici.
{% endhint %}

Parmi ce concept d'ontologie existe les **ontologies pour le web sémantique**. Il s'agit d'un type d'ontologie particulier qui s'intéresse principalement à la cohérence logique et l'expressivité des éléments décrits pour **permettre le raisonnement automatique**. Pour cela, les langages de description de ces ontologies utilisent la [logique de premier ordre](fol.md) pour modéliser l'univers $$\Omega$$ qui nous intéresse. Conséquemment, les ontologies permettent de simuler le processus cognitif humain, ce qui les rend très pratiques pour les incorporer dans des processus d'IA où l'explicabilité et les relations complexes sont de mises.

{% hint style="info" %}
Dans la suite, par le terme **ontologie**, on fera référence aux ontologies du web sémantiques.
{% endhint %}

![Visualisation de l'ontologie Friend of a Friend (FOAF) grâce à WEBVOWL](assets/foaf_vowl.png)

Élaborer un ontologie requiert **une connaissance experte du domaine** afin d'en saisir toutes les subtilités. C'est une étape complexe, qui doit être méthodiquement effectuer. En ce ses, [Powell, 2015](../REF.md/#powell2015) propose des étapes classiques pour l'élaboration d'une ontologie :

1. Identifier votre **taxonomie** -- quels sont les éléments, les sous-éléments...
2. Quels éléments **non pas de relation** avec d'autres ?
3. Quels éléments "**héritent**" (*i.e.* sont des) de plusieurs éléments ?
4. Quels sont les **caractéristiques uniques** définissant un individu ?
5. Quels sont les **caractéristiques mesurables** d'un élément ?
6. Quels éléments sont **décrit par** l'entremise d'**autres éléments** ?

{% hint style="danger" %}
Ne pas se reposer sur des experts lors de l'élaboration d'une ontologie, c'est prendre le risque d'introduire un fossé sémantique entre votre modélisation et la "réalité terrain", qui peut se traduire par la non-adoption de l'ontologie ou pire, à des raisonnements faux !
{% endhint %}

Ci dessous, nous passons en revue les éléments principaux d'une ontologie.

## Vocabulaire

Une ontologie modélise un univers $$\Omega$$ qui est un sous-ensemble du monde observable, et où il est possible de manipuler ses entités constitutives pour opérer des raisonnements logiques, à travers un graphe $$\mathcal{G}=(V,E)$$.

Ces "entités constitutives" se décomposent en deux types principaux : les **classes** $$V$$ qui sont les objets, les éléments dont on veut parler (*e.g.* arbre, feuille, racine) et les **propriétés** $$E$$ qui expriment les relations qui existent entre les classes (*e.g.* un arbre est une (`subClassOf`) plante).

Dans l'image précédente de l'ontologie *FOAF*, les classes sont représentées par les cercles bleues, et les relations par les flêches labélisées avec des encart rectangulaire.

{% hint style="info" %}
Le point de départ d'une propriété s'appelle le **domaine**, et le point d'arrivé la **portée**. C'est élément sont descriptifs de la propriété et c'est ce qui lui donne tout son sens ! Par exemple, une relation $$\text{isSeekingNutrient} : \text{Racine} \mapsto \text{Nutrient}$$ indique que tout ce qui est une racine à une propriété allant dans nutriment (qui est un ensemble constitué des classes Azotes, Potassium, etc.).
{% endhint %}

On remarque également des propriétés avec des encarts verts pointant vers des cases oranges. Ces propriétés sont des "propriétés de données" (Data property) qui permettent d'expliciter des caractéristiques d'une classe (par exemple `firstName`) *via* l'utilisation de littéraux (les boites oranges).

## A-BOX vs T-BOX

Vous pouvez être en train de vous demander au vue du discours précédent comment différencier les concepts que l'on souhaite modéliser (*e.g.* le concept d'arbre), et la modélisation de l'observation d'un **individu spécifique** de cette classe (*e.g.* l'arbre dans votre jardin).

Les ontologies, grossièrement, sont découpée en deux parties pour permettre cela : une partie "conceptuelle", appelée **T-Box** (pour terminological component) et une partie "faits", appelée **A-Box** (pour assertion component), pour modéliser les instances des classes et raisonner dessus.

### Terminological component

En un sens, la **T-Box** représente les règles de votre modélisation. C'est ici que tous les concepts sont décrits : les classes et les propriétés de ces classes. Toutes les descriptions y sont donc génériques.

{% hint style="warning" %}
Les descriptions y sont peut être génériques, mais elles peuvent être très précises aussi. Le tout est de **ne pas parler d'instances spécifiques** dans cette partie. Par exemple, décrire l'écorce de *Eucalyptus deglupta* dans les "grande lignes" ne pose pas de soucis, même si elle est très atypique, puisqu'elle est commune à toute l'espèce.
{% endhint %}

*Exemple :*
> ```
> Tous les Étudiants sont des Personnes
> ```
> 
> ```
> Il y a deux types de personnes : des XX (Femme) et des XY (Homme).
> ```

### Assertion component

La **A-Box** contient la modélisation de tous vos individus, **en fonction** de votre T-Box. Aussi, pour les décrire vous utiliserez des classes et des relations qui proviennent de votre description.

*Exemple :*
> ```rdf
> Bob est un Homme
> ```
> 
> ```rdf
> Cette feuille appartient à mon arbre de jardin, qui est un *Cinnamomum Camphora*.
> ```

Concrètement, en utilisant la T-Box conjointement avec votre A-Box, cela permet de raisonner sur les faits que vous décrivez et d'inférer de nouvelles informations, ainsi que de trouver d'éventuelles incohérences dans votre ontologie (ou dans la définition de vos individus).

{% hint style="success" %}
Dans le dernier exemple, si votre T-Box est bien construite, par exemple :

* $$\text{foillageOf} : \text{Leaf} \mapsto \text{Tree}$$ (**T-Box**)
* $$\text{hasLeafType} : \text{Cinnamomum_Camphora} \mapsto ( \text{MonoLob_Leaf} \wedge \text{Ovoïd} )$$ (**T-Box**)
* $$\text{foillageOf} : \text{MyLeaf} \mapsto \text{MyCinnamomum}$$ (**A-Box**)
* $$\text{typeOf} : \text{MyCinnamomum} \mapsto \text{Cinnamomum_Camphora}$$ (**A-Box**)

Alors, on peut savoir que la feuille que j'ai ramassé de mon camphrier est mono-lobé et ovoïde, et que le camphrier est un arbre, qu'il possède des racines, produit du camphre, etc.
{% endhint %}

Cela nous permet de tirer des conclusions sur l'univers décrit.

Attention cependant, car c'est l'union des deux box qui constitue l'univers que vous tentez de modéliser, t.q. : $$\Omega = \text{T-Box} \cup \text{A-Box}$$.

## Spécialisation des propriétés

Spécialiser une propriété la conditionne et lui induit des contraintes supplémentaires qui seront utilisées lors du raisonnement.

Ce n'est pas obligatoire d'attribuer à une spécialisation à une propriété, mais cela peut aider à renforcer les contraintes d'intégrité du système que vous êtes en train de décrire.

Une peut peut avoir aucune, une ou plusieurs spécialisations à la fois. Elles sont au nombres de 5 :

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
> Ici, on définit en plus de la propriété `locatedIn` la propriété `adjacentRegion`, qui à pour domaine une `Region` et une portée de `Region`. La région `MendocinoRegion` est définie comme adjacente à la région `SonomaRegion`. On peut donc **en déduire** que `SonomaRegion` est aussi adjacente à `MendocinoRegion`. Par contre, il n'y a pas symétricité pour la propriété `locatedIn CaliforniaRegion` concernant `SonomaRegion` : on n'a aucune information d'où elle est située.

### Fonctionnelle

Si une propriété $$P$$ est spécifiée comme fonctionnelle, alors $$\forall x, y, z$$ on a : $$P(x,y) \wedge P(y,z) \rightarrow y = z$$.

Autrement dit, si une propriété est fonctionnelle, le terme en portée est **"unique"**.

{% hint style="info" %}
Bien qu'on puisse dire que la portée est unique, cela n'empêche pas d'exprimer $$P(x,y)$$ et $$P(x,z)$$, au contraire. Si on sait que la `chocolatine` est une `viennoiserie`, mais pas le `petitPain`, que la fonction `mange` est fonctionnelle, et qu'on a un moment `mange(Bob,chocolatine)` puis plus tard `mange(Bob,petitPain)`, on en déduit que `chocolatine = petitPain` **ET** que `petitPain` est une `viennoiserie`. Pratique, en plus de mettre fin au conflit (on sait tous que la chocolatine est la vraie).
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
> Ici la fonction `hasVintageYear` (a un millésime) est fonctionnelle. Un vin ne peut avoir qu'un seul millésime, pas plus. Aussi, une entité `Vintage` ne pourra être associée sémantiquement qu'à une seule année `VintageYear` via la propriété `hasVintageYear`.

{% hint style="danger" %}
Bien que la différence soit ténue, être fonctionnelle n'est pas pareil que de limiter une classe à n'avoir une propriété qu'avec une autre classe ! La fonctionnalité, c'est plutôt une "unicité sémantique de l'individualisation de la portée d'un prédicat".
{% endhint %}

### Inverse de

Si une propriété $$P1$$ est spécifiée comme l'inverse de $$P2$$, alors $$\forall x, y$$ on a : $$P1(x,y) \leftrightarrow P2(y,x)$$.

Autrement dit, on sait que si $$P1$$ est vraie, alors $$P2$$ l'est elle aussi.

*Exemple :*
> ```rdf
> <owl:ObjectProperty rdf:ID="hasMaker">
>   <rdf:type rdf:resource="&owl;FunctionalProperty" />
> </owl:ObjectProperty>
>   
> <owl:ObjectProperty rdf:ID="producesWine">
>   <owl:inverseOf rdf:resource="#hasMaker" />
> </owl:ObjectProperty>
> ```
> Ici, les vins ont des vignerons qui les fabriquent (dans la définition de `Wine` elle est restreinte aux vignerons `Winerys`). On indique ensuite que `producesWin` est l'inverse `hasMaker` (d'être produit par).

### Fonctionnelle Inverse

Si une propriété $$P$$ est spécifiée comme inverse fonctionnelle, alors $$\forall x, y, z$$ on a : $$P(y,x) \wedge P(z,x) \rightarrow y = z$$.

Autrement dit, l'unicité sémantique s'établie sur le domaine de la propriété, et non plus sur sa portée (à l'inverse de [Fonctionnelle](owl.md/#fonctionnelle)).

{% hint style="warning" %}
L'inverse d'une propriété fonctionnelle doit toujours être qualifiée comme fonctionnelle inverse, et pas seulement l'[Inverse de](owl.md/#inverse-de), afin de conserver la sémantique véhiculée.
{% endhint %}

*Exemple :*
> ```rdf
> <owl:ObjectProperty rdf:ID="hasMaker" />
>   
> <owl:ObjectProperty rdf:ID="producesWine">
>   <rdf:type rdf:resource="&owl;InverseFunctionalProperty" />
>   <owl:inverseOf rdf:resource="#hasMaker" />
> </owl:ObjectProperty>                                     ¬ 
> ```
> Notez que dans cette exemple, la propriété précédemment vue dans [Inverse de](owl/#inverse-de) est qualifiée ici comme fonctionnelle inverse. Puisqu'un vin ne peut être produit que par une seule classe, si pour un vin donné on se retrouve avec deux producteurs différents, cela veut dire que c'est forcément les mêmes.

## Représentation des ontologies

Brièvement, une ontologie est décrite à l'aide de deux langage principaux : [RDF (Ressource Description Framework)](https://fr.wikipedia.org/wiki/Resource_Description_Framework) et [RDFS (Ressource Description Framework - Schema)](https://fr.wikipedia.org/wiki/RDF_Schema). Ces deux langages sont standardisés par la W3C et largement utilisé. 

{% hint style="info" %}
[Turtle](https://www.w3.org/TR/2014/REC-turtle-20140225/) est aussi largement répandu pour décrire des ontologies. Il s'agit d'un langage bijectif avec RDF qui permet de représenter de manière un peu moins verbeux les différents triplets RDF et aussi plus "humainement" compréhensible.
{% endhint %}

### RDF

RDF est un langage de description de multigraphes orientés qui gère la description et les méta-données pour le web sémantique. Sa syntaxe est simple et repose toujours sur trois éléments : **sujet**, **prédicat** et **objet**, et s'exprime généralement comme `prédicat(sujet, objet)`.

Il est injectif dans la logique de premier ordre ; plus particulièrement il est bijectif avec la logique de premier ordre positive, conjonctive et existentielle :

$$\text{predicat(sujet,objet)} \leftrightarrow \exists \text{sujet}, \exists \text{objet}, \text{predicat(sujet,objet)}$$

Les différentes entités de l'ontologie (*i.e.* classes et propriétés) sont toutes identifiées par une **[URI](https://fr.wikipedia.org/wiki/Uniform_Resource_Identifier)**, ce qui permet de les déréférencer en ligne (il peut tout de même y avoir des entités anonymes).

### RDFS

RDFS quand à lui est un langage **extensible** qui permet de structurer les ressources décrites en RDF et apporte des concepts de bases pour les ontologies : `rdfs:subClassOf` et `rdfs:Class` pour les classes et surtout `rdfs:domain` et `rdfs:range` pour les propriétés !

Il est donc le canvas de votre ontologie.

{% hint style="success" %}
RDFS (et un schéma de votre ontologie) est donc indispensable pour que votre ontologie soit utilisable !
{% endhint %}

### Triplestore, requêtage et endpoints

Grâce à RDF/RDFS, il est possible d'entreposer vos ressources dans des bases de données appelées **triplestores**.

L'avantage de cela, ce qu'il devient possible d'utiliser les mécanismes d'implications et de logiques dans vos requêtes pour consulter vos données. Le langage de requête standardisé pour consulter du RDF/S est **SPARQL**.

L'implication de tout cela est que vous êtes en train d'assister à l'émergence d'un écosystème à part entière, où des ressources fortement sémantisées peuvent être hébergées dans des bases de données, et dont le format permet de raisonner avec la machine.

Si une base de données externe vous autorise à consulter ses données avec des requêtes SPARQL, on dit alors que c'est un **endpoints** SPARQL. Grosso modo, vous pouvez requêter la base avec des requêtes et récupérer les données qui vous intéresse, tout en pouvant exploiter les implications logiques.

{% hint style="info" %}
[MusicBrainz](https://wiki.musicbrainz.org/LinkedBrainz) et [WikiData](https://query.wikidata.org/) sont deux exemples bien connus.
{% endhint %}
