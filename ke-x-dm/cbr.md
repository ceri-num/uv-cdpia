# Case Based Reasoning

## Introduction

Le **Case Based Reasoning** (CBR), ou raisonnement à partir de cas (RàPC), est un type de raisonnement basé sur la remémoration et l'adaptation d'anciens cas rencontrés et résolus pour en résoudre de nouveaux, souvent **similaires** [[Kolodner92]](../REF.md/#kolodner92).

Il repose sur des principes d'ingénieries des connaissances pour trouver les cas similaires et les adapter, et de l'aide à la décision pour expliquer pourquoi le cas proposé semble adéquat à la situation et prendre en compte les corrections utilisateurs aux propositions automatisées.

*Exemple :*
> Vous voulez faire un repas amical où plusieurs régimes alimentaires se côtoient. Vous vous souvenez de ce que vous avez individuellement préparé aux invités les dernières fois, et essayez de trouver l'union de ce qui convient le mieux, en faisant les modifications nécessaires.
> 
> Au cours du repas, vous prenez notes des éventuelles remarques de vos convives et, une fois le repas terminé, vous notez le tout pour plus tard -- au cas où : procédés, recettes et feedbacks. Voila, vous faîtes du CBR !

## Overview

Le CBR est un type de raisonnement très intuitif, basé sur un "meta-schéma" cognitif humain, qui se décompose en quatres grandes parties :

* Remémoration
* Réutilisation
* Révision
* Mémorisation

![Schéma du raisonnement à partir de cas, réalisée par Lin Ma](assets/cbr_lifecycle.png)

{% hint style="info" %}
Le cycle du CBR est généralement associé aux utilisateurs. Les cas solutionnés sont ainsi souvent proposés à l'utilisateur pour prise de décision et révision avant d'être appliqué. Néanmoins, le CBR s'applique aussi à des systèmes automatisés : l'action est directement effectuée, et la réaction de l'environnement sur le système est déduit dans la révision pour future correction.
{% endhint %}

### Remémoration

L'étape de remémoration (*retrieve* dans la schéma) consiste à accéder à la base de cas et à **chercher** des cas qui sont **similaires** au cas actuellement rencontré.

Plusieurs techniques peuvent être utilisées pour procéder à cette phase de remémoration, comme par exemple les graphes de concepts ou la *FOL*. Elle n'en reste pas moins une phase délicate : de la qualité de la phase d'identification de cas similaires dépend l'ensemble de la résolution du problème.

Il est donc nécessaire de ne pas être trop générique, ni trop spécifique dans cette étape ; d'être capable de traîter des cas qui sont contextuellement différents mais similaires ; de classer correctement (bonne métrique) les cas sélectionner.

### Réutilisation

L'étape de réutilisation consiste à se servir du cas remémoré pour résoudre le problème actuel. Pour cela, l'ancien cas est souvent **adapté** pour correspondre exactement à la situation. Cette adaptation, là encore, si automatisé (comme souvent), repose bien souvent sur des mécanismes d'ingénierie des connaissances, notamment les [chaînages](../ke/fol.md/#inference).

Néanmoins, l'on peut très bien imaginer un système demandant à l'utilisateur quel cas lui semble le plus adapter dans une situation donnée. 

### Révision

L'étape de révision consiste à modifier le cas (remémoré + réutilisé/adapté automatiquement) *a posteriori* de son utilisation. Cela permet de corriger le cas pour qu'il soit le plus approprié possible à la situation, une fois le retour de l'environnement effectué (par exemple, freiner plus fort).

Cette étape reçoit de manière coutumière l'intervention humaine, qui permet d'ajuster finement les règles et les paramètres du cas aux observations. Le cas peut éventuellement être rejoué pour de meilleur résultat, si le contexte le permet.

### Mémorisation

L'étape de mémorisation consiste à enregistrer le nouveau cas dans la base de connaissance du système, pour servir aux prochaines remémorations. En fonction du système, la mémorisation peut faire intervenir des mécanismes de référencement complexes, pour améliorer la phase de remémoration.