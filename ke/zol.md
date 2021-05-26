# Logique propositionnelle (ou d'ordre 0)

une proposition est une assertion ayant une valeur de vérité déterminable.
Valeur de vérité : 0 ou 1

Par exemple, $$1+1=2$$, Lille est dans le Sud de la France...

À quoi ça sert ? représenter logiquement de l'information, et pouvoir tirer des conclusions de l'agencement de ces proposition lorsqu'on les évalue.

Allons survoler un peu tout ça.

## Syntaxe
* Un ensemble de propositions, appelé variables de proposition, lettre propositionnelles : `P`, `Q`, `R`... Cet ensemble est supposé *infini* mais dénombrable.
* Des opérateurs (ou connecteur), qui permettent de relier les clauses les unes les autres, et construire des propositions plus complexe. Les connecteurs les plus courants sont :

| Symbole   |  Connecteur  |
|:----------:|:-------------:|
| $$\wedge$$ |  ET (**Conjonction**) |
| $$\vee$$ |  OU (**Disjonction**)   |
| $$\rightarrow$$ | **Implication** |
| $$\leftrightarrow$$ | **Équivalence** |
| $$\lnot$$ | NON (**Négation**) |

{% hint style="info" %}
L'ordre d'application des connecteurs a une importance. Pour spécifier l'ordre, l'on utilise également les parenthèses **(** et **)**
{% endhint %}

## Table de vérité

### Conjonction

| $$P$$   |  $$Q$$  | $$P \wedge Q$$ |
|:----------:|:-------------:|:-------------:|
| 0 | 0 | 0 | 
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### Disjonction

| $$P$$   |  $$Q$$  | $$P \vee Q$$ |
|:----------:|:-------------:|:-------------:|
| 0 | 0 | 0 | 
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### Négation

| $$P$$   |  $$\lnot P$$ |
|:----------:|:-------------:|
| 0 | 1 | 
| 1 | 0 |

### Implication

| $$P$$   |  $$Q$$  | $$P \rightarrow Q$$ |
|:----------:|:-------------:|:-------------:|
| 0 | 0 | 1 | 
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |


{% hint style="info" %}
$$P \rightarrow Q$$ est équivalent à $$(\lnot P \vee Q)$$.
{% endhint %}

Cette relation permet d'exprimer la relation **SI... ALORS**. Pour qu’il y ait implication, il faut donc au final que :
* l’antécédent (ici $$P$$) soit une condition suffisante du conséquent ;
* le conséquent (ici $$Q$$) soit une condition nécessaire de l’antécédent.

{% hint style="success" %}
Autrement on peut lire également pour que $$P$$, il suffit de $$Q$$. Autrement dit, du vrai n'implique jamais du faux, et du faux implique n'importe quoi.
{% endhint %}

*Exemple :*
> Il neige donc le sol est blanc. La neige est une condition suffisante ($$P$$) d’un sol blanc. Il suffit qu’il neige pour que le sol soit blanc ($$P \rightarrow Q$$). Le sol blanc est une condition nécessaire ($$Q$$) de la neige. Il faut (nécessité) que le sol soit blanc pour qu’il neige. C’est nécessaire mais pas suffisant : si on a que cette information (le sol blanc), il ne neige pas forcément.

### Équivalence

| $$P$$   |  $$Q$$  | $$P \leftrightarrow Q$$ |
|:----------:|:-------------:|:-------------:|
| 0 | 0 | 1 | 
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Cette relation permet d'exprimer la relation **si et seulement si**. Quand on a un, on a automatiquement l'autre ; quand l'on a pas l'un, on a automatiquement pas l'autre.

{% hint style="info" %}
$$P \leftrightarrow Q$$ est équivalent à $$P \rightarrow Q \wedge Q \rightarrow P$$.
{% endhint %}

{% hint style="success" %}
Cela peut se lire aussi comme $$P$$ est une condition nécessaire et suffisante à $$Q$$.
{% endhint %}

## Exemples théoriques

### Si... Alors... Sinon

**Si** $$P$$ **Alors** $$Q$$ **Sinon** $$R$$ est une structure ternaire, mais décomposable avec les opérateurs vu ci-avant. 

{% hint style="info" %}
On a vue que $$P \rightarrow Q$$ permet d'exprimer la notion de **SI...ALORS**
{% endhint %}

On peut alors l'exprimer comme : $$(P\rightarrow Q)\vee(\lnot P \rightarrow R)$$

### Un exemple bien de chez nous

> Un français, de mauvaise humeur, ça râle !

Soit **Français** $$\mapsto P$$, **Humeur** $$\mapsto Q$$, **Râler** $$\mapsto R$$

On a alors $$(P \wedge \lnot Q) \rightarrow R$$ qui *tient*, en cela que cette proposition n'exclue que râler peut survenir dans d'autres situation, ou alors que d'autres nationalités ont propension à le faire également, par exemple. 

{% hint style="danger" %}
Alors que $$(P \wedge \lnot Q) \leftrightarrow R$$ signifie que râler est une propriété unique n'appartenant qu'aux français de mauvais humeur (puisque : $$((P \wedge \lnot Q) \rightarrow R) \wedge (R \rightarrow (P \wedge \lnot Q))$$.
{% endhint %}

## Système déductif
Grâce à la logique d'ordre 0, on peut d'ores et déjà envisager des systèmes déductifs à base de règles pour raisonner.

### *Modus Ponen*
Il s'agît d'une règle primitive de raisonnement faisant intervenir l'implication, que l'on nomme également *règle du détachement*. L'idée est de déduire la valeur de $$Q$$ d'après $$P$$ et l'implication de $$P$$ par rapport à $$Q$$.

1. On à la proposition $$P \rightarrow Q$$, dîte **prémisse majeure** ;
2. la proposition $$P$$, qualifiée de **prémisse mineure** ;
3. et enfin $$Q$$, qui est la **conclusion**.

Elle se note :

$$
    \begin{equation}
        \frac{P \hspace{0.5cm} P \rightarrow Q}{Q}
    \end{equation}
$$

Cela se lit de $$P$$ et de $$P \rightarrow Q$$ en est déduit $$Q$$. Autrement dit, en affirmant $$P\rightarrow Q$$ et $$P$$, l'on peut affirmer $$Q$$.

{% hint style="danger" %}
Quand on a dit $$P \rightarrow Q$$, on a pas dit $$P$$, ni $$Q$$ ; aussi, on ne connaît ni la valeur de vérité de $$P$$ et encore moins de $$Q$$. Si $$P$$ est ensuite posée à vraie, alors on peut en déduire que la proposition $$Q$$ est vraie également.
{% endhint %}

{% hint style="info" %}
Il existe également la contraposée du *modus ponen*, le *modus tollen* (*i.e.* $$(\lnot P \wedge (\lnot P\rightarrow \lnot Q))\rightarrow Q$$).
{% endhint %}

### Syllogisme par Hypothèse
Il s'agît d'exploiter les règles de détachement pour constituer des hypothèses et créer des implications simples pour réaliser ce qu'on appelle une démonstration en déduction naturelle.

*Exemple :*
> "S'il fait beau ($$P$$) j'irai grimper cette après-midi ($$Q$$). Si je vais grimper cette après-midi ($$Q$$), je n'irai pas travailler ($$R$$). Donc, s'il fait beau je n'irai pas travailler."

Ce qui s'exprime comme :

$$
    \begin{equation}
        \frac{ \frac{P \hspace{0.5cm} P \rightarrow Q}{Q} \hspace{0.5cm} Q\rightarrow R}{R}
    \end{equation}
$$

{% hint style="info" %}
Une démonstration en déduction naturelle repose sur un arbre de preuve, comme ci dessus.
{% endhint %}

## Résumé

Grâce à la logique de proposition, on commence déjà à **modéliser l'information** sous forme de propositions. Cela nous permet déja de raisonner avec ces propositions, et ainsi produire de la connaissance supplémentaire (*cf.* Modus Ponen).

Néanmoins, la logique de proposition, comme son nom l'indique, ne permet pas d'exprimer de la variabilité.

La phrase suivante n'est pas une proposition par exemple :

> Mon entreprise est en Europe

En effet, en fonction de l'entreprise, une telle proposition devient alors soit vraie, soit fausse, soit "indéterminée" (*e.g.* en Russie). L'on ne parle plus de proposition mais de **prédicat**.