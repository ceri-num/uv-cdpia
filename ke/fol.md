# Logique des prédicats

Avec la logique des prédicats (ou d'ordre 1) on passe un cran au dessus en terme d'expressivité des phrases, puisqu'il est possible d'exprimer, entre autre, la notion de variabilité dans une proposition, qui se nomme alors un **prédicat**. Incidemment, elle devient plus difficilement satisfiable.

Avec cette logique, on peut totalement modéliser des systèmes complexes, capables d'exploiter une base de connaissances et de faits pour raisonner efficacement et produire de l'information.

{% hint style="info" %}
Une base de connaissance est un ensemble de faits connus (*i.e.* des constantes), par exemple Homme(Socrate).
{% endhint %}

Formellement, un prédicat se définit comme :
> une expression linguistique qui peut être reliée à un ou plusieurs éléments du domaine pour former une phrase [[source]](https://fr.wikipedia.org/wiki/Calcul_des_pr%C3%A9dicats).

## Syntaxe

### Alphabet

* Un ensemble de termes variables, toujours infini mais dénombrables : $$x,y,z\ldots$$
* un ensemble de termes constants, qui peut être soit $$\emptyset$$, soit $$a,b,c\ldots$$
* Un ensemble de prédicats $$\mathcal{P}$$ (ou relations) : $$P, Q, R\ldots$$
* Un un ensemble de connecteurs : $$\wedge$$, $$\vee$$, $$\lnot$$, $$\rightarrow$$ $$\ldots$$
* Deux quantificateurs : $$\forall$$ (**pour tous**) et $$\exists$$ (**il existe**)

{% hint style="danger" %}
L'ordre des quantificateurs est important !
* $$\forall x\exists y \hspace{0.1cm} x+1 > y$$
* $$\exists y\forall x \hspace{0.1cm} x+1 > y$$ !! Jamais vrai 
{% endhint %}


### Arité
$$\forall P \in \mathcal{P}$$, $$P$$ possède une arité (*i.e.* le nombre de variables et de constantes qui interviennent).

Par exemple :
* le prédicat `pere` est dit **dyadique** puisque pour être le père de quelqu’un, deux entités sont concernés. On note cela 
```c++
pere(x,y) //x est le père de y
```
* le prédicat `grand` est dit **monoadique** puisqu'un seul individu est concerné. Il s'exprime comme
```c++
grand(x) //x est grand 
```

### Formule
Une formule du calcul des prédicats (*i.e.* mot) se définit par **induction**.

{% hint style="info" %}
Vous avez un [Glossaire](../GLOSSARY.md) à disposition.
{% endhint %}

Soit $$n_P$$ un poids associé à chaque prédicat $$P \in \mathcal{P}$$. $$P(x_1,x_2\dots x_n)$$ est une formule *ssi* $$P$$ est de poids $$n$$.

*Exemple :*
> * `pere(x,y)` est un mot ;
> * `grand(x,y)` n'est pas un mot puisqu'il est monadique.

De plus, une formule qui ne possède **que** des **variables liées** est appelée un **enoncé**.

* Lorsqu'une variable est associée à un quantificateur (*e.g.* $$\forall x, P(x)$$), on dit qu'elle est liée ;
* Inversement, lorsqu'une variable n'est pas associée à un quantificateur, on dit qu'elle est libre.

L'exemple ci-après illustre le célèbre syllogisme de Socrate, que l'on ne peut pas expliquer en *ZOL*.
> $$\forall x \hspace{0.1cm}  (humain(socrate) \wedge (humain(x) \rightarrow mortel(x)))\rightarrow mortel(socrate)$$

## Règles
pere <->


Fol \cite{smullyan1995first}