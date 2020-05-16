---
title: Linear Algebra Notation
layout: page
---
$$
\newcommand{\ihat}{\hat{\boldsymbol{\imath}}}
\newcommand{\jhat}{\hat{\boldsymbol{\jmath}}}
\newcommand{\khat}{\hat{\boldsymbol{k}}}
\newcommand{\vc}[1]{\mathbf{#1}}
$$

* This will become a table of contents (this text will be scraped).
{:toc}

# Notation

## Abstract Form

There are several ways to abstractly represent vectors:

|Name|Notation|Description|
|-|-|-|
| bar | $ \bar{u} $ | often easiest to use when writing by hand |
| arrow on top | $ \vec{u} $ | also easy to use when writing by hand |
| bold | $ \mathbf{u} $ | avoids busy combinations such as $ \dot{\vec{u}} $, often used in textbooks |

Also we have:

|Name|Symbol|Description|
|-|-|-|
| unit vectors | $ \hat{a} $ | always has a magnitude of 1  |
| basis vectors | $ \boldsymbol{e_1}, \boldsymbol{e_2}, ..., \boldsymbol{e_n} $ | |


## Component Form

Component form represents vectors in terms of coordinates with respect to a certain basis vectors (or axis). There are several ways to do this.

### Basis Vector Notation

Basis vectors are often referred to as $ \vc{e_1}, \vc{e_2}, \vc{e_3} $, etc.

The unit vectors $ \ihat $, $ \jhat $ and $ \khat $ vectors are called the standard basis vectors for $ \mathbb{R}3 $ and represent a magnitude 1 vector in each of the x, y and z directions respectively. An example of a vector written using _unit vector notation_ is:

$$ \vec{u} = 3 \ihat + 4\jhat-2\khat $$

### Ordered Set Notation

For convenience writing by hand, it's fairly common to see vector components written in ordered set notation. This is quite efficient in terms of vertical space on the page as well.

|Name|Notation|
|-|-|
| angle brackets | $ \vec{u} = \langle 3, 4, -2 \rangle = 3 \ihat + 4 \jhat - 2 \khat $ |  
| parenthesis | $ \vec{u} = (3, 4, -2) = 3 \ihat + 4 \jhat - 2 \khat $ |

### Matrix Notation

Vectors are most often represented as an n x 1 matrix, called a column vector or matrix.

|Name|Notation|
|-|-|
| column | $ \vec{u} = \begin{pmatrix} 3 \\ 4 \\ -2 \end{pmatrix} = 3 \ihat + 4 \jhat - 2 \khat $ | |  
| column via transpose | $ \vec{u} = \begin{pmatrix} 3 & 4 & -2 \end{pmatrix}^\intercal = 3 \ihat + 4 \jhat - 2 \khat $ | simplifies writing column vectors in-line with other text|


While vectors can be represented in row form also, column form tends to be preferred. This may be because we like to think of matrices as functions, such as $ f(x) $, operating on an input vector and so, when using matrices, we try to emulate this notation using $ Mv $ rather than $ vM $. This requires we use column vectors because of the way matrix multiplication is defined.

Note that there are two equivalent notations for matrices: $ ( ) $, $ [ ] $. So for example, these column vectors are equivalent: $
\begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} $ and these row vectors are equivalent $ \begin{pmatrix} 1 & 0 & 0 \end{pmatrix} = \begin{bmatrix} 1 & 0 & 0 \end{bmatrix} $. It's ok to use either bracket style. Some people think parenthesis notation is easier/faster to write by hand and less easily confused with the vertical bars the denote determinants.

### Importance of Column vs Row Vectors

You should be careful when dealing with this, because the rules of matrix multiplication apply. For example, some operations with the "same" vector but written in different ways may lead to different results. For example:

$$
\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}
\begin{bmatrix} 0 & 1 & 0 \end{bmatrix}
= \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}
$$

However, if we write the first vector as a row, we get a different result:

$$ \begin{bmatrix} 1 & 0 & 0 \end{bmatrix} \begin{bmatrix} 0 & 1 & 0 \end{bmatrix} = 0 $$

Another example is vectors $ \mathbf{u} = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix} $  $ \mathbf{v} = \begin{bmatrix} 4 \\ 5 \\ 6 \end{bmatrix} $ which cannot be be multiplied as written and must be re-written as either:

$$
\mathbf{u} \cdot \mathbf{v} = \mathbf{u}^\intercal \mathbf{v}
= \begin{bmatrix} 1 & 2 & 3 \end{bmatrix}
\begin{bmatrix} 4 \\ 5 \\ 6 \end{bmatrix}
= 1 \cdot 4 + 2 \cdot 5 + 3 \cdot 6
$$

or

$$
\mathbf{u} \otimes \mathbf{v} = \mathbf{u} \mathbf{v}^\intercal
= \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}
\begin{bmatrix} 4 & 5 & 6 \end{bmatrix}
= \begin{bmatrix}
1 \cdot 4 & 1 \cdot 5 & 1 \cdot 6 \\
2 \cdot 4 & 2 \cdot 5 & 2 \cdot 6 \\
3 \cdot 4 & 3 \cdot 5 & 3 \cdot 6 \\
\end{bmatrix}
$$

Similarly this product is well defined and works without complication:

$$
\begin{bmatrix} 2 & 1 & 0 \\ 8 & 0 & 1 \\ 3 & 1 & 1 \end{bmatrix}
\begin{bmatrix} 1 \\ 1 \\ 2 \end{bmatrix}
$$

... but this product makes no sense and cannot be done:

$$
\begin{bmatrix} 2 & 1 & 0 \\ 8 & 0 & 1 \\ 3 & 1 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 1 & 2 \end{bmatrix}
$$
