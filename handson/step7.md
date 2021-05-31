# Classification et vérification (Étape 7)

## Utiliser le raisonneur

L'ontologie n'est pas considérée comme complète tant que vous ne l'avez pas classifiée et vérifiée ! Autrement dit, vous allez lancer un raisonneur sur votre ontologie, et ce dernier va vérifier les inconsistences éventuelles, identifier les éléments qui sont équivalents, trouver de nouvelles informations à partir de votre base de faits, etc.

{% hint style="danger" %}
Il est important de sauvegarder votre travail ! Faîtes le ici si ce n'est pas déjà fait !
{% endhint %}

Choisissez d'abord votre raisonneur. Pour ce faire `Reasonner > HermiT 1.4.3` (c'est le raisonneur par défaut).

Une fois le raisonneur sélectionné, lancez le en faisant `Reasonner > start reasonner`. Vous verrez alors que des informations supplémentaires vont apparaître petit à petit (surbrillance jaune dans la zone de description), notamment au niveau du champ `subClassOf` de vos Pizza.

Dans l'[étape 6](step6.md/#fermons-notre-margarita) concernant la margarita vous avez réalisé l'étape optionnelle 5, vous devriez alors avoir un champ rouge qui apparaît :

![La classe `Marguerita_pizza` rencontre un problème.](assets/marga_broken.png)

En réalité, il n'existe aucun individu capable de respecter les quatres critères que nous avons énoncé, d'où le `owl:Nothing`. Pour régler se problème, vous devez **relaxer** les contraintes : remplacer le `and` par un `or`, relancer votre raisonneur, et votre ontologie passe ! Yay !

{% hint style="info" %}
Pourquoi cette erreur ? Rappelez vous : nous avons définis `Cheese_topping` et `Tomato_topping` comme disjoint, donc ils ne peut pas y avoir d'intersection ! Il est fort ce raisonneur !
{% endhint %}

## Un mot sur la A-Box

Tout ce tutoriel s'est concentré sur la **T-Box** de l'ontologie, autrement dit toutes les classes et les propriétés qui existent entre ces classes et qui modélisent votre problème.

Brièvement tout de même, explorons comment faire.

Imaginons que nous voulions parler d'une margarita spécifique, présente sur notre table, achetée à Douai : il ne s'agit alors plus d'un concept, mais d'une instance de ce concept - un **individu**. On remarque que sur notre margarita, il y a des morceaux de viande.

1. Dans l'onglet `Individual` créez un nouvel individu (appelez le comme vous voulez)
2. Dans son champ `Type` dans la zone de description, ajoutez `Margarita_Pizza`
3. Rajouter un nouvel individu qui représentera la viande sur votre pizza
4. Sélectionnez à nouveau votre pizza, et dans le champ `Object Property Assertions` ajoutez : `has_topping leNomDeVotreIndividuQuiReprésenteLaViande`
5. Lancer de nouveau le raisonneur.

**Badabomm !**

![Le raisonneur nous explique pourquoi il trouve que notre ontologie est inconsistante avec notre observation.](assets/individual_oops.png)

Ce qu'il se passe, c'est que votre raisonneur remarque une incohérence entre votre T-Box et votre observation dans la A-Box : une margarita **ne peut pas avoir** de viande. Aussi, votre raisonneur vous dit qu'il y a un problème. Pour le corriger, il suffit simplement de ne mettre que de la garniture tomate ou fromage.

Vous pouvez aller beaucoup plus loin ! Par exemple, créez un nouvel individu qui représentera le goût de votre pizza, mais ne lui donnez pas de type. Retirez également le type de votre individu garniture, et rajoutez lui l'`Object Property Asserstions` : `has_spiciness votreGoutIndividu`.

Relancer le raisonneur, et vous verrez que ce dernier à inférer le type des éléments !

## Dump de l'ontologie

Vous trouverez si dessous le dump de l'ontologie qu'on a construit au fil de ce tuto (avec une magnifique faute d'orthographe à viande !). Elle est aussi accessible [ici](../owl/pizza.owl).

```
@prefix : <http://www.semanticweb.org/alexis/ontologies/pizza#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix xml: <http://www.w3.org/XML/1998/namespace> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@base <http://www.semanticweb.org/alexis/ontologies/pizza> .

<http://www.semanticweb.org/alexis/ontologies/pizza> rdf:type owl:Ontology .

#################################################################
#    Object Properties
#################################################################

###  http://www.semanticweb.org/alexis/ontologies/pizza#has_base
:has_base rdf:type owl:ObjectProperty ;
          rdfs:subPropertyOf :relational_property ;
          rdf:type owl:FunctionalProperty ,
                   owl:InverseFunctionalProperty ;
          rdfs:domain :Pizza ;
          rdfs:range :Pizza_base .


###  http://www.semanticweb.org/alexis/ontologies/pizza#has_spiciness
:has_spiciness rdf:type owl:ObjectProperty ;
               rdfs:subPropertyOf :modifier_property ;
               rdf:type owl:FunctionalProperty ;
               rdfs:domain :Pizza_topping ;
               rdfs:range :Spiciness_value .


###  http://www.semanticweb.org/alexis/ontologies/pizza#has_topping
:has_topping rdf:type owl:ObjectProperty ;
             rdfs:subPropertyOf :relational_property ;
             rdf:type owl:InverseFunctionalProperty ;
             rdfs:domain :Pizza ;
             rdfs:range :Pizza_topping .


###  http://www.semanticweb.org/alexis/ontologies/pizza#modifier_property
:modifier_property rdf:type owl:ObjectProperty ;
                   rdfs:subPropertyOf owl:topObjectProperty .


###  http://www.semanticweb.org/alexis/ontologies/pizza#relational_property
:relational_property rdf:type owl:ObjectProperty ;
                     rdfs:subPropertyOf owl:topObjectProperty .


#################################################################
#    Classes
#################################################################

###  http://www.semanticweb.org/alexis/ontologies/pizza#Anchovy_topping
:Anchovy_topping rdf:type owl:Class ;
                 rdfs:subClassOf :Fish_topping ,
                                 [ rdf:type owl:Restriction ;
                                   owl:onProperty :has_spiciness ;
                                   owl:someValuesFrom :Mild_value
                                 ] ;
                 owl:disjointWith :Tuna_topping .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Cheese_topping
:Cheese_topping rdf:type owl:Class ;
                rdfs:subClassOf :Pizza_topping .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Cheesy_pizza
:Cheesy_pizza rdf:type owl:Class ;
              rdfs:subClassOf [ owl:intersectionOf ( :Pizza
                                                     [ rdf:type owl:Restriction ;
                                                       owl:onProperty :has_topping ;
                                                       owl:minQualifiedCardinality "2"^^xsd:nonNegativeInteger ;
                                                       owl:onClass :Cheese_topping
                                                     ]
                                                   ) ;
                                rdf:type owl:Class
                              ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Domain_entity
:Domain_entity rdf:type owl:Class .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Fish_topping
:Fish_topping rdf:type owl:Class ;
              rdfs:subClassOf :Pizza_topping .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Fruit_topping
:Fruit_topping rdf:type owl:Class ;
               rdfs:subClassOf :Pizza_topping .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Gorganzolla_topping
:Gorganzolla_topping rdf:type owl:Class ;
                     rdfs:subClassOf :Cheese_topping ,
                                     [ rdf:type owl:Restriction ;
                                       owl:onProperty :has_spiciness ;
                                       owl:someValuesFrom :Mild_value
                                     ] ;
                     owl:disjointWith :Mozzarella_topping .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Ham_topping
:Ham_topping rdf:type owl:Class ;
             rdfs:subClassOf :Meet_topping ,
                             [ rdf:type owl:Restriction ;
                               owl:onProperty :has_spiciness ;
                               owl:someValuesFrom :Medium_value
                             ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Hot_and_spicy_pizza
:Hot_and_spicy_pizza rdf:type owl:Class ;
                     owl:equivalentClass [ owl:intersectionOf ( :Pizza
                                                                [ rdf:type owl:Restriction ;
                                                                  owl:onProperty :has_topping ;
                                                                  owl:someValuesFrom :Spicy_topping
                                                                ]
                                                              ) ;
                                           rdf:type owl:Class
                                         ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Hot_value
:Hot_value rdf:type owl:Class ;
           rdfs:subClassOf :Spiciness_value .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Independent_entity
:Independent_entity rdf:type owl:Class ;
                    rdfs:subClassOf :Domain_entity ;
                    owl:disjointWith :Value .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Marguerita_pizza
:Marguerita_pizza rdf:type owl:Class ;
                  rdfs:subClassOf :Pizza ,
                                  [ rdf:type owl:Restriction ;
                                    owl:onProperty :has_topping ;
                                    owl:someValuesFrom :Mozzarella_topping
                                  ] ,
                                  [ rdf:type owl:Restriction ;
                                    owl:onProperty :has_topping ;
                                    owl:someValuesFrom :Tomato_topping
                                  ] ,
                                  [ rdf:type owl:Restriction ;
                                    owl:onProperty :has_topping ;
                                    owl:allValuesFrom [ rdf:type owl:Class ;
                                                        owl:unionOf ( :Mozzarella_topping
                                                                      :Tomato_topping
                                                                    )
                                                      ]
                                  ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Medium_value
:Medium_value rdf:type owl:Class ;
              rdfs:subClassOf :Spiciness_value .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Meet_topping
:Meet_topping rdf:type owl:Class ;
              rdfs:subClassOf :Pizza_topping .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Mild_value
:Mild_value rdf:type owl:Class ;
            rdfs:subClassOf :Spiciness_value .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Mozzarella_topping
:Mozzarella_topping rdf:type owl:Class ;
                    rdfs:subClassOf :Cheese_topping ,
                                    [ rdf:type owl:Restriction ;
                                      owl:onProperty :has_spiciness ;
                                      owl:someValuesFrom :Mild_value
                                    ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Onion_topping
:Onion_topping rdf:type owl:Class ;
               rdfs:subClassOf :Vegetable_topping ,
                               [ rdf:type owl:Restriction ;
                                 owl:onProperty :has_spiciness ;
                                 owl:someValuesFrom :Mild_value
                               ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Pepperoni_topping
:Pepperoni_topping rdf:type owl:Class ;
                   rdfs:subClassOf :Meet_topping ,
                                   [ rdf:type owl:Restriction ;
                                     owl:onProperty :has_spiciness ;
                                     owl:someValuesFrom :Medium_value
                                   ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Pineapple_topping
:Pineapple_topping rdf:type owl:Class ;
                   rdfs:subClassOf :Fruit_topping ,
                                   [ rdf:type owl:Restriction ;
                                     owl:onProperty :has_spiciness ;
                                     owl:someValuesFrom :Mild_value
                                   ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Pizza
:Pizza rdf:type owl:Class ;
       rdfs:subClassOf :Independent_entity .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Pizza_base
:Pizza_base rdf:type owl:Class ;
            rdfs:subClassOf :Independent_entity .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Pizza_topping
:Pizza_topping rdf:type owl:Class ;
               rdfs:subClassOf :Independent_entity .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Soja_steak_topping
:Soja_steak_topping rdf:type owl:Class ;
                    rdfs:subClassOf :Vegetable_topping ,
                                    [ rdf:type owl:Restriction ;
                                      owl:onProperty :has_spiciness ;
                                      owl:someValuesFrom :Medium_value
                                    ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Spiciness_value
:Spiciness_value rdf:type owl:Class ;
                 rdfs:subClassOf :Value ,
                                 [ rdf:type owl:Class ;
                                   owl:unionOf ( :Hot_value
                                                 :Medium_value
                                                 :Mild_value
                                               )
                                 ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Spicy_beef_topping
:Spicy_beef_topping rdf:type owl:Class ;
                    rdfs:subClassOf :Meet_topping ,
                                    [ rdf:type owl:Restriction ;
                                      owl:onProperty :has_spiciness ;
                                      owl:someValuesFrom :Hot_value
                                    ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Spicy_topping
:Spicy_topping rdf:type owl:Class ;
               owl:equivalentClass [ owl:intersectionOf ( :Pizza_topping
                                                          [ rdf:type owl:Restriction ;
                                                            owl:onProperty :has_spiciness ;
                                                            owl:someValuesFrom :Hot_value
                                                          ]
                                                        ) ;
                                     rdf:type owl:Class
                                   ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Thick_crust_base
:Thick_crust_base rdf:type owl:Class ;
                  rdfs:subClassOf :Pizza_base ;
                  owl:disjointWith :Thin_crust_base .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Thin_crust_base
:Thin_crust_base rdf:type owl:Class ;
                 rdfs:subClassOf :Pizza_base .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Tomato_topping
:Tomato_topping rdf:type owl:Class ;
                rdfs:subClassOf :Vegetable_topping ,
                                [ rdf:type owl:Restriction ;
                                  owl:onProperty :has_spiciness ;
                                  owl:someValuesFrom :Mild_value
                                ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Tuna_topping
:Tuna_topping rdf:type owl:Class ;
              rdfs:subClassOf :Fish_topping ,
                              [ rdf:type owl:Restriction ;
                                owl:onProperty :has_spiciness ;
                                owl:someValuesFrom :Mild_value
                              ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Value
:Value rdf:type owl:Class ;
       rdfs:subClassOf :Domain_entity .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Vegan_pizza
:Vegan_pizza rdf:type owl:Class ;
             rdfs:subClassOf [ owl:intersectionOf ( :Pizza
                                                    [ rdf:type owl:Class ;
                                                      owl:complementOf [ rdf:type owl:Restriction ;
                                                                         owl:onProperty :has_topping ;
                                                                         owl:someValuesFrom [ rdf:type owl:Class ;
                                                                                              owl:unionOf ( :Cheese_topping
                                                                                                            :Fish_topping
                                                                                                            :Meet_topping
                                                                                                          )
                                                                                            ]
                                                                       ]
                                                    ]
                                                  ) ;
                               rdf:type owl:Class
                             ] .


###  http://www.semanticweb.org/alexis/ontologies/pizza#Vegetable_topping
:Vegetable_topping rdf:type owl:Class ;
                   rdfs:subClassOf :Pizza_topping .


#################################################################
#    Individuals
#################################################################

###  http://www.semanticweb.org/alexis/ontologies/pizza#myMargueritaBoughtAtDouai
:myMargueritaBoughtAtDouai rdf:type owl:NamedIndividual ,
                                    :Marguerita_pizza ;
                           :has_topping :theBeefOnMyMarguerita .


###  http://www.semanticweb.org/alexis/ontologies/pizza#tasteOfMyTopping
:tasteOfMyTopping rdf:type owl:NamedIndividual .


###  http://www.semanticweb.org/alexis/ontologies/pizza#theBeefOnMyMarguerita
:theBeefOnMyMarguerita rdf:type owl:NamedIndividual ;
                       :has_spiciness :tasteOfMyTopping .


#################################################################
#    General axioms
#################################################################

[ rdf:type owl:AllDisjointClasses ;
  owl:members ( :Cheese_topping
                :Fish_topping
                :Fruit_topping
                :Meet_topping
                :Vegetable_topping
              )
] .


[ rdf:type owl:AllDisjointClasses ;
  owl:members ( :Ham_topping
                :Pepperoni_topping
                :Spicy_beef_topping
              )
] .


[ rdf:type owl:AllDisjointClasses ;
  owl:members ( :Hot_value
                :Medium_value
                :Mild_value
              )
] .


[ rdf:type owl:AllDisjointClasses ;
  owl:members ( :Onion_topping
                :Soja_steak_topping
                :Tomato_topping
              )
] .


[ rdf:type owl:AllDisjointClasses ;
  owl:members ( :Pizza
                :Pizza_base
                :Pizza_topping
              )
] .


###  Generated by the OWL API (version 4.5.9.2019-02-01T07:24:44Z) https://github.com/owlcs/owlapi
```