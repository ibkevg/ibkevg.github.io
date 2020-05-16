---
title: Geometric Product
layout: page
---
$$
\newcommand{\ihat}{\hat{\boldsymbol{\imath}}}
\newcommand{\jhat}{\hat{\boldsymbol{\jmath}}}
\newcommand{\khat}{\hat{\boldsymbol{k}}}
\newcommand{\vc}[1]{\mathbf{#1}}
\newcommand{\inner}[2]{ \langle #1, #2 \rangle }
\newcommand{\abs}[1]{ \lvert #1 \rvert }
$$

## Dot Product versus our Criteria for a "Good Product"

Let's review the dot product against our expectations:

1. Useful applications  
**Yes** We showed above that the dot product can be used to determine the angle between vectors, is useful to test perpendicularity and parallelity, find projections onto basis or other vectors, etc.  
Also an example from physics: $ W = \vc{F} \cdot \vc{d} $  
1. Geometric meaning  
**Yes** The dot product can be viewed as a projection-based multiply.
1. Works the same as regular number multiplication  
**Yes**
The dot product obeys the commutative, associative and distributive properties.
1. Support division that works the same as regular number division  
**No** The dot product loses information in producing it's scalar result. You can't start with a scalar dot product result and recover one of the initial vectors.
1. Regular number multiplication should be just a special case  
**Yes** If a vector has a single dimension, then the dot project becomes identical to 
1. Should be closed under multiplication, just like reals and complex numbers  
**No** Dot product of two vectors produces a scalar. Why doesn't it produce a vector? Because it is symmetrical, you could think of it as a projection of either vector onto the other. So it would have to choose the dirction of one of the vectors.

So it's a pretty good multiply but not perfect.

## Cross Product versus our Criteria for a "Good Product"

Let's review the cross product against our expectations:

1. Useful applications  
**TBD**
1. Geometric meaning  
**TBD**
1. Works the same as regular number multiplication  
**TBD**
1. Support division that works the same as regular number division  
**TBD**
1. Regular number multiplication should be just a special case  
**TBD**
1. Should be closed under multiplication, just like reals and complex numbers  
**TBD**

So it's a pretty good multiply but not perfect.


# Combining Dot and Cross Products

While dot and cross products on their own don't satisfy our requirements for multiplying vectors, we have some hints that suggest the two may be combined. Perhaps this combination does?

Earlier we learned that $ \vc{u} \cdot \vc{v} \propto \cos{\theta} $ and $ \vc{u} \times \vc{v} \propto \sin{\theta} $. This suggests we may find a pythagorean relation, $ \sin^2 + \cos^2 = 1 $, between them.

Also, suggesting a possible relation are the multiplication tables for both kinds of products.

Dot product multiplication table:
$$
\begin{array}{c|c|c|c}
\cdot & e_1 & e_2 & e_3 \\ \hline
e_1 & 1 & 0 & 0 \\ \hline
e_2 & 0 & 1 & 0 \\ \hline
e_3 & 0 & 0 & 1
\end{array} 
$$

Cross product multiplication table:
$$
\begin{array}{c|c|c|c}
\times & e_1 & e_2 & e_3 \\ \hline
e_1 & 0 & e_3 & -e_2 \\ \hline
e_2 & -e_3 & 0 & e_1 \\ \hline
e_3 & e_2 & -e_1 & 0
\end{array} 
$$

## Lagrange's Identity

Lagrange's Identity shows us that the dot and cross products are two parts of a greater whole. It is analogous to Pythagoras Theorem but for vector multiplication.

$$
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
= {\lvert \vc{a} \times \vc{b} \rvert}^2 + \lvert \vc{a} \cdot \vc{b} \rvert^2
$$

We can find this using:

$$
\begin{aligned}
\lvert \vc{a} \times \vc{b} \rvert
&= \lvert \vc{a} \rvert \lvert\vc{b} \rvert \sin{\theta} \\
{\lvert \vc{a} \times \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 \sin{\theta}^2 \\
{\lvert \vc{a} \times \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 (1 - \cos{\theta}^2) \\
{\lvert \vc{a} \times \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - ({\lvert \vc{a} \rvert} {\lvert\vc{b} \rvert} \cos{\theta} )^2 \\
{\lvert \vc{a} \times \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - \lvert \vc{a} \cdot \vc{b} \rvert^2 \\
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
&= {\lvert \vc{a} \times \vc{b} \rvert}^2 + \lvert \vc{a} \cdot \vc{b} \rvert^2
\end{aligned}
$$

Or starting with the dot product:

$$
\begin{aligned}
\lvert \vc{a} \cdot \vc{b} \rvert
&= \lvert \vc{a} \rvert \lvert\vc{b} \rvert \cos{\theta} \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 \cos{\theta}^2 \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 (1 - \sin{\theta}^2) \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - ({\lvert \vc{a} \rvert} {\lvert\vc{b} \rvert} \sin{\theta} )^2 \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - \lvert \vc{a} \times \vc{b} \rvert^2 \\
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
&= {\lvert \vc{a} \times \vc{b} \rvert}^2 + \lvert \vc{a} \cdot \vc{b} \rvert^2
\end{aligned}
$$



# Multiplying Two Quarternions

Quarternions are an extension of complex numbers. Here we write $ \vc{u} $ and $ \vc{v} $ as pure vector quarternions:

$$
\begin{aligned}
\vc{u} &= u_x \ihat + u_y \jhat + u_z \khat \\
\vc{v} &=  v_x \ihat + v_y \jhat + v_z \khat
\end{aligned}
$$

Think of i, j and k analogous to x, y, and z.

$$
\begin{aligned}
\vc{u} \vc{v}
= \; &\begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix}
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix} \\
= \;
&u_x v_x \ihat \ihat + u_x v_y \ihat \jhat + u_x v_z \ihat \khat +\\
&u_y v_x \jhat \ihat + u_y v_y \jhat \jhat + u_y v_z \jhat \khat +\\
&u_z v_x \khat \ihat + u_z v_y \khat \jhat + u_z v_z \khat \khat
\end{aligned}
$$

Just like $ \vc{i} $ for imaginary numbers, imagine $ \vc{j}, \vc{k} $ are similar:

$$ \ihat \ihat = \jhat \jhat = \khat \khat =  \ihat \jhat \khat = -1 $$

We can now derive $ \ihat \jhat $:

$$\begin{aligned}
\ihat \jhat \khat &= -1 \\
\ihat \jhat \khat \khat &= -1 \khat \\
\ihat \jhat (-1) &= -1 \khat \\
\ihat \jhat &= \khat \\
\end{aligned}$$

A similar process produces:

$$ \ihat \jhat = \khat \;\;\; \jhat \khat = \ihat  \;\;\; \khat \ihat = \jhat $$

Next:

$$\begin{aligned}
(\jhat \khat)(\khat \ihat) &= \ihat \jhat \\
\jhat (\khat \khat) \ihat &= \khat \\
\jhat (-1) \ihat &= \khat \\
\jhat \ihat &= -\khat \\
\end{aligned}$$

A similar process produces:

$$ \khat \jhat = -\ihat \;\;\; \jhat \ihat = -\khat \;\;\; \ihat \khat = -\jhat $$

Now we can substitute to get:

$$
\begin{aligned}
\vc{u} \vc{v}
= \;
&-(u_x v_x + u_y v_y + u_z v_z) \\
&+ (u_y v_z - u_z v_y) \ihat \\
&+ (u_z v_x - u_x v_z) \jhat \\
&+ (u_x v_y - u_y v_x) \khat \\
\vc{u} \vc{v} = \; &-(\vc{u} \cdot \vc{v}) + (\vc{u} \times \vc{v})
\end{aligned}
$$
