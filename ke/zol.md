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
L'ordre d'application des connecteurs a une importance. Pour spécifier l'ordre, l'on utilise également les parenthèses ( et )
{% endhint %}

## Table de vérité

### Conjonction

| P   |  Q  | $$P \wedge Q$$ |
|:----------:|:-------------:|:-------------:|
| 0 | 0 | 0 | 
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### Disjonction

| P   |  Q  | $$P \vee Q$$ |
|:----------:|:-------------:|:-------------:|
| 0 | 0 | 0 | 
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### Négation

| P   |  $$\lnot P$$ |
|:----------:|:-------------:|
| 0 | 1 | 
| 1 | 0 |

### Implication

| P   |  Q  | $$P \rightarrow Q$$ |
|:----------:|:-------------:|:-------------:|
| 0 | 0 | 1 | 
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |


{% hint style="info" %}
$$P \rightarrow Q$$ est équivalent à $$(\lnot P \vee Q)$$.
{% endhint %}

Cette relation permet d'exprimer la relation **SI... ALORS**. Pour qu’il y ait implication, il faut donc au final que :
* l’antécédent (ici P) soit une condition suffisante du conséquent ;
* le conséquent (ici Q) soit une condition nécessaire de l’antécédent.

{% hint style="success" %}
Autrement on peut lire également pour que P, il suffit de Q. Autrement dit, du vrai n'implique jamais du faux, et du faux implique n'importe quoi.
{% endhint %}

Exemple :
Il neige donc le sol est blanc. La neige est une condition suffisante (P) d’un sol blanc. Il suffit qu’il neige pour que le sol soit blanc ($$P \rightarrow Q$$). Le sol blanc est une condition nécessaire (Q) de la neige. Il faut (nécessité) que le sol soit blanc pour qu’il neige. C’est nécessaire mais pas suffisant : si on a que cette information (le sol blanc), il ne neige pas forcément.

### Équivalence

| P   |  Q  | $$P \leftrightarrow Q$$ |
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
Cela peut se lire aussi comme P est une condition nécessaire et suffisante à Q.
{% endhint %}