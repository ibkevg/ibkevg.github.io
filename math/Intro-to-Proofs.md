---
title: Intro to Proofs
layout: page
---

# References

## Books
1. [How to Prove It: A Structured Approach, 2nd edition](https://www.amazon.com/How-Prove-Structured-Daniel-Velleman/dp/0521675995), Daniel J. Velleman, 2006.
1. [Book of Proof](https://www.amazon.com/Book-Proof-Richard-Hammack/dp/0989472108), Revised Edition, Richard Hammack. Freely available at the author's website: [link](http://www.people.vcu.edu/~rhammack/BookOfProof/)
1. [Proofs and Fundamentals: A First Course in Abstract Mathematics, 2nd edition](https://www.amazon.com/Proofs-Fundamentals-Abstract-Mathematics-Undergraduate/dp/1441971262), 2nd edition, Ethan Bloch, 2011.

## Summary Notes
1. [Logic and Proof](http://www.madscitech.org/tm/lap.pdf), George E. Hrabovsky. 


# Velleman

## 1. Sentential Logic

### 1.1 Deductive Reasoning and Logical Connectives

**Connective Symbols**


| Symbol | Meaning | Notes |
| :--: | :--: | |
| $$ \vee $$ | logical or | $$ P \vee Q $$ sometimes called the *disjunction* of P and Q |
| $$ \wedge $$ | logical and | $$ P \wedge Q $$ sometimes called the *conjunction* of P and Q |
| $$ \neg $$ | logical not | $$ \neg P $$ sometimes called the *negation* of P |

**Notes:**
+ Order of operations: $$ \neg P \vee Q $$ means $$ (\neg P) \vee Q $$
+ Some expressions have hidden logical words. Consider $$ 3 \leq \pi < 4 $$.
  + This means: $$ 3 \leq \pi $$ and $$ \pi < 4 $$  
  + Which means $$ [( 3 < \pi ) \vee ( 3 = \pi )] \wedge ( \pi < 4 ) $$

### 1.2 Truth Tables

**Equivalence Laws**


| Name | Statement | is equivalent to...|
| :--     | :--     | :--  |
| DeMorgan's laws | $$ \neg( P \wedge Q) $$ | $$ \neg P \vee \neg Q $$ |
|  | $$ \neg( P \vee Q) $$ | $$ \neg P \wedge \neg Q $$ |
| Commutative laws | $$ P \wedge Q $$ | $$ P \wedge Q $$ |
|  | $$ P \vee Q $$ | $$ Q \vee P $$ |
| Associative laws | $$ P \wedge (Q \wedge R) $$ | $$ (P \wedge Q) \wedge R $$ |
|  | $$ P \vee (Q \vee R) $$ | $$ (P \vee Q) \vee R $$ |
| Idempotent laws | $$ P \wedge P $$ | $$ P $$ |
|  | $$ P \vee P $$ | $$ P $$ |
| Distributive laws | $$ P \wedge ( Q \vee R ) $$ | $$ (P \wedge Q) \vee (P \wedge R) $$ |
|  | $$ P \vee ( Q \wedge R ) $$ | $$ (P \vee Q) \wedge (P \vee R) $$ |
| Absorbtion laws | $$ P \vee ( P \wedge Q ) $$ | $$ P $$ |
|  | $$ P \wedge ( P \vee Q) $$ | $$ P $$ |
| Double negation | $$ \neg\neg P $$ | $$ P $$ |

Notes:
+ *tautology* - a formula that is always true (e.g. $$ P \vee \neg P $$)
+ *contradiction* - a formula that is always false (e.g. $$ P \wedge \neg P $$)


### 1.3 Variables and Sets

A *set* is a collection of objects.
+ objects in the collection are called the *elements* of the set.
+ the ordering of elements in a set is unimportant
+ elements can even appear in a set multiple times
+ two sets are equal if they have exactly the same elements (again, order doesn't matter)
+ $$ \{3, 7, 14\}, \{7, 3, 14\}, \{14, 7, 3\} $$ are all equal (ie. the same set)


| Symbol | Means | |
| $$ \in $$ | is an element of | if $$ A = \{3,7,14\} $$ then $$ 7 \in A $$ |
| $$ \notin $$ | not an element of |  $$ 11 \notin A $$|

**Set Builder Notation**

$$ A = \{ 6, 7, 8, ... \} $$ could also be written using set builder notation as:  
$$ A = \{ x \in \mathbb{Z} \mid x > 5 \} $$ (which is written by some people as $$ A = \{ x  \in \mathbb{Z} : x > 5 \} $$). It means "A is the set of all integers greater than 6"
