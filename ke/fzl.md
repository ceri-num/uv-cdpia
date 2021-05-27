# Logique Floue (Fuzzy Logic)

Encore de la logique ?!
{% hint style="info" %}
Et oui, il y a beaucoup d'autres logiques, allant de celles simples comme celle des propositions à la logique dynamique introduisant la notion d'action en plus (par exemle $$(x>6)\rightarrow [x:=x*2](x>12)$$), utilisé pour la vérification de programme informatique.
{% endhint %}

Néanmoins, la plupart de ces logiques sont qualifiés de **crisp** (oui, oui, comme les gâteux apéro) : ils prennent une valeur de vérité dans un interval **discret** sémantisé *a priori*, généralement {`0`,`1`}, avec `0 = FAUX` et `1 = VRAI`.

Les ensembles flous et la logique floue s'établissent plutôt en rupture de toutes ces logiques *crisp*. L'idée est de travailler avec un interval **continue** de valeur, compris entre `[0;1]`, qui représente l'appartenance d'un concept à un ensemble donné.

Intuitivement, pour comprendre le besoin, l'on peut se poser la question du tas de sable : À quel moment, en empilant un par un les grains de sables, l'on peut parler de **tas** de sable ? La logique floue apporte une modélisation mathématique à cette question.

*Exemple :*
> La variable `Bob` appartient à l'ensemble `grand`, *t.q.* grand(Bob), avec un **degré** de 0.67, et la variable `Anna` avec un degré de 0.35. Avec ces information, l'on peut commencer à faire du raisonnement.

{% hint style="warning" %}
Le notion de degré est différente de celle de probabilité ! La probabilité est **crisp** ! En effet, si vous avez $$P(x)=0.67$$ t.q. $$x \in \text{grand}$$ cela signifie que `x` a 67% de chance d'être grand (*i.e.* que ce soit vrai), et 23% de chance d'être faux. En *fuzzy*, il est, pour une unité, "0.67 grand et 0.23 petit".
{% endhint %}

Pour définir le degré d'appartenance d'une variable `x` (*e.g.* une mesure), on procède à une **fuzzification**. On peut ensuite faire des opérations mathématiques simulant les connecteurs vue dans la [ZOL](zol.md) et la [FOL](fol.md). Néanmoins, il n'est pas possible d'interpréter avec des valeurs de vérité les résultats : il faut tout d'abord les faire sortir de ces ensembles flous, ce qu'on appel la **defuzzification**, pour ensuite leur attribuer une valeur de vérité.

{% hint style="danger" %}
Les connecteurs logiques ne sont plus définis universellement !
{% endhint %}

## Fuzzification

Dans les grandes lignes, on définit $$s_1,\ldots ,s_n, n \in \mathbb{N}$$ comme des ensemble flous, t.q. $$s \in \mathcal{S}$$ (l'ensemble de nos ensembles flous). On définit également $$m_s$$, la fonction d'appartenance à l'ensemble flou (*membership function*) $$s$$* comme $$m:\mathbb{R} \mapsto [0;1]$$.

La fonction de fuzzification $$\mu: x \mapsto [0;1]^n$$ consiste à prendre une variable x et la projeter dans nos ensembles flous, pour définir un degré d'appartenance pour chacun des ensembles.

![Degré d’appartenance à des ensemble distinct de la variable mesurée. (©McGillUniv)](assets/fuzzy.png)

Avec cette approche, les informations deviennent humainement interprétables. Il est même possible d'introduire des modificateurs sémantiques (*e.g.* peu, énormément,etc.).

## Pipeline de la FZL

![Pipeline logique dans l’espace flou et defuzzyfication, par Ferhat Pakdamar](assets/Graphical-presentation-of-the-max-min-inference-method-with-crisp-inputs.png)