# Étude du problème (Étape 1)

Étudier un problème fait partie des bonnes pratiques à avoir, surtout lorsque votre problème est complexe et/ou que vous envisagez de déployer un système complexe pour le résoudre.

Ici, vous n'aurez pas encore besoin de Protégé : une feuille et un crayon suffisent !

## Les grandes lignes de création d'ontologies

Le [guide de McGuinness](https://protege.stanford.edu/publications/ontology_development/ontology101-noy-mcguinness.html) propose une démarche simple pour créer une ontologie. 

1. Déterminer le domaine et la portée de l'ontologie (autrement dit, ce qu'elle va concerner). Utiliser les 5 W peut offrir un premier cadre de réflexion ;
2. Faire un état de l'art des ontologies déjà existante ; 
{% hint style="success" %}
C'est là tout l'intérêt des ontologies web : se reposer sur l'existant, et les enrichir juste de ce qu'il faut pour pouvoir parler de son domaine. De cette manière, si tout le monde sait qu'un `foaf:person` représente la notion de personne, pas besoin de la créer dans la votre ! Autant réutiliser cette classe (et tout ce qu'elle implique ;).
{% endhint %}
3. Dresser le catalogues des éléments importants de votre ontologies ;
4. Définir les classes de l'ontologie, et la hiérarchie associée (approche top-down, bottom-up, mixée) ;
5. Définir les propriétés existante dans l'ontologie ;
6. Créer les instances (A-BOX) de l'ontologie ;

## Retour sur notre problème

Reprenons notre problème de la pizza. Notre objectif est de créer une ontologie pour décrire un large ensemble de pizza, et de pouvoir expliquer qu'une pizza est composée de différentes garnitures, etc...

### Vue d'ensemble

Si on dresse le catalogue des éléments importants, on aurait alors :

* La pizza en elle même
* La pâte utilisée
* La garniture
* Le type de la pizza (Margarita, etc)

En plus de cela, les propriétés sont :

* une pizza a obligatoirement une pâte
* une pizza a obligatoirement une garniture

### Vue détaillée

Maintenant que l'on a une vue globale de notre domaine de travail, on peut se résoudre à enrichir notre catalogue d'individu plus spécifique.

Par exemple, pour la pâte, on aurait :

| Type de pâte   |
|:----------:|
| Épaisse |
| Fine |

Pour la garniture par exemple :

| Garniture |
|:---------:| 
| Tomate |
| Mozarella |
| Boeuf épicé |
| Pepperoni |

{% hint style="warning" %}
Dans Protégé, préférez des noms sans accent et sans espace, comme `tomate_gar` ou `thick_crust`.
{% endhint %}

Pour les propriétés, on en a deux principales, à savoir :

| Propriété |
|:---------:| 
| hasTopping |
| hasCrust |

## Résumé 

Dans tous vos problèmes, la première chose à faire c'est de comprendre votre problème et de lister les éléments qui interviennent en son sein.

Dans la suite, nous verrons comment utiliser Protégé pour construire notre ontologie !