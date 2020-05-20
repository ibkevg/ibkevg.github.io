---
title: Emergence of the Dot and Wedge Products
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

* This will become a table of contents (this text will be scraped).
{:toc}

Here we find equations that allow us to determine if two vectors are parallel or perpendicular. Although we start only with the basic laws of triangles like Pythagorus and the law of cosines, we will find that the equations for the dot and wedge products emerge.

We will then compare the multiplication tables for the dot and wedge products and find that they each address orthogonal parts, suggesting that the two may be combined.

Finally we will look at Lagrange's Identity that further points in this direction.

# Dot Product Emergence

The dot product relation emerges naturally from Pythagoras' theorem. To see this happen, we will explore perpendicular vectors, which have the special property of having a dot product of zero.

Consider vectors $ \vc{a} $ and $ \vc{b} $ where $ \vc{a} $ is perpendicular to $ \vc{b} $. Because $ \vc{a} \perp \vc{b} $, we can think of them as the opposite and adjacent sides of a right triangle and therefore, applying Pythagoras we get:

$$
\begin{aligned}
|\vc{s}|^2_{perp}
&=  \lvert \vc{a} \rvert^2  +  \lvert \vc{b} \rvert^2 \\
|\vc{s}|^2_{perp}
&=  (a_x^2 + a_y^2 + a_z^2)  +  (b_x^2 + b_y^2 + b_z^2)
\end{aligned}
$$

Also, for any triangle, 2 of the vectors that form the sides of the triangle must sum to the other. We can arbitrarily choose $ \vc{s} = \vc{a} + \vc{b} $ or $ \vc{s} = \vc{a} - \vc{b} $ :

$$ |\vc{s}|^2 = (a_x+b_x)^2 + (a_y+b_y)^2 + (a_z+b_z)^2 $$

Since both equations are describing the same triangle, $ \abs{\vc{s}}^2 = \abs{\vc{s}}^2_{perp} $, and thus we can write:

$$
\begin{aligned}
(a_x+b_x)^2 + (a_y+b_y)^2 + (a_z+b_z)^2
&= (a_x^2 + a_y^2 + a_z^2)  +  (b_x^2 + b_y^2 + b_z^2) \\
a_x^2 + 2a_x b_x + b_x^2 +
a_y^2 + 2a_y b_y + b_y^2 + 
a_z^2 + 2a_z b_z + b_z^2
&= a_x^2 + a_y^2 + a_z^2 + b_x^2 + b_y^2 + b_z^2 \\
2a_x b_x + 2a_y b_y + 2a_z b_z
&= 0 \\
a_x b_x + a_y b_y + a_z b_z &= 0
\end{aligned}
$$

This is consistent with the definition of the dot product which is 0 when the vectors are perpendicular:

$$ \vc{a} \cdot \vc{b} = a_x b_x + a_y b_y + a_z b_z $$

# Cross Product Emergence

> The cross product emerges naturally from Pythagoras' theorem. To see how this works, below we will take advantage of the fact that the cross product of two parallel vectors is zero.

Now let's consider the case where $ \vc{a} $ is parallel to $ \vc{b} $. We can't directly apply Pythagoras but we can apply the law of cosines:

$$ |\vc{s}|^2 = |\vc{a}|^2 + |\vc{b}|^2 - 2|\vc{a}||\vc{b}|\cos S $$

and because our vectors are parallel, $ S = 180^\circ $ making $ \cos 180^\circ = -1 $, which gives:

$$
\begin{aligned}
|\vc{s}|^2_{parallel}
&=  |\vc{a}|^2 + |\vc{b}|^2 + 2|\vc{a}||\vc{b}| \\
&=  (a_x^2 + a_y^2 + a_z^2)  +  (b_x^2 + b_y^2 + b_z^2) + 2|\vc{a}||\vc{b}|
\end{aligned}
$$

Also, for any triangle, the sum of any $ \vc{a} $ and $ \vc{b} $ is $ \vc{s} = \vc{a} + \vc{b} $, therefore:

$$ |\vc{s}|^2 = (a_x + b_x)^2 + (a_y + b_y)^2 + (a_z + b_z)^2 $$

We can equate these two expressions, $ \abs{\vc{s}}^2 = \abs{\vc{s}}^2_{parallel} $, when $ \vc{a} \parallel \vc{b} $:

$$
\begin{aligned}
2a_x b_x + 2a_y b_y + 2a_z b_z &= 2|\vc{a}||\vc{b}| \\
a_x b_x + a_y b_y + a_z b_z &=  \sqrt{a_x^2 + a_y^2 + a_z^2}\sqrt{b_x^2 + b_y^2 + b_z^2} \\
(a_x b_x + a_y b_y + a_z b_z)^2 &=  (a_x^2 + a_y^2 + a_z^2)(b_x^2 + b_y^2 + b_z^2) \\
\end{aligned}
$$

Expanding these expressions and cancelling terms, we get:

$$
2a_x b_x a_y b_y + 2a_x b_x a_z b_z + 2a_y b_y a_z b_z
= (a_x b_y)^2 + (a_x b_z)^2 + (a_y b_x)^2 + (a_y b_z)^2 + (a_z b_x)^2 + (a_z b_y)^2
$$

Notice that we can gather terms and re-write this as

$$ (a_x b_y - b_x a_y)^2  +  (b_x a_z - a_x b_z)^2  +  (a_y b_z - b_y a_z)^2  =  0 $$

This sum of squares equals zero only when $ \vc{a} \parallel \vc{b} $ and is consistent with the definition of the cross product:

$$ \vc{a} \times \vc{b}
= \begin{bmatrix}
a_y b_z - b_y a_z \\
a_y b_z - b_y a_z \\
a_x b_y - b_x a_y
\end{bmatrix}
$$

Also as we saw previously, the dot product of two vectors is 0 if the vectors are perpendicular. We can use this to confirm the following:

that $ \vc{a} \times \vc{b} $ is perpendicular to $ \vc{a} $:

$$
\begin{aligned}
\vc{a} \cdot (\vc{a} \times \vc{b})
&= \begin{bmatrix} a_x, a_y, a_z \end{bmatrix} \cdot 
\begin{bmatrix}
a_y b_z - b_y a_z \\
a_y b_z - b_y a_z \\
a_x b_y - b_x a_y
\end{bmatrix} = 0 \\
&= a_x a_y b_z - a_x b_y a_z  +  a_y b_x a_z - a_y a_x b_z  +  a_z a_x b_y - a_z b_x a_y \\
&= 0
\end{aligned}
$$

that $ \vc{a} \times \vc{b} $ is perpendicular to $ \vc{b} $:

$$
\begin{aligned}
\vc{b} \cdot (\vc{a} \times \vc{b})
&= \begin{bmatrix} b_x, b_y, b_z \end{bmatrix} \cdot 
\begin{bmatrix}
a_y b_z - b_y a_z \\
a_y b_z - b_y a_z \\
a_x b_y - b_x a_y
\end{bmatrix} = 0 \\
&= b_x a_y b_z - b_x b_y a_z  +  b_y b_x a_z - b_y a_x b_z  +  b_z a_x b_y - b_z b_x a_y \\
&= 0 
\end{aligned}
$$

# Combining Dot and Cross/Wedge Products

The multiplication tables for dot and wedge products suggest that the two produce orthogonal results that may possibly be combined into a more general form of vector multiplication.

Dot product multiplication table entries are zero when $ \vc{e}_i \neq \vc{e}_j $:

$$
\begin{array}{c|c|c|c}
\cdot & e_1 & e_2 & e_3 \\ \hline
e_1 & 1 & 0 & 0 \\ \hline
e_2 & 0 & 1 & 0 \\ \hline
e_3 & 0 & 0 & 1
\end{array} 
$$

Cross product multiplication table entries are zero when $ \vc{e}_i = \vc{e}_j $:

$$
\begin{array}{c|c|c|c}
\times & e_1 & e_2 & e_3 \\ \hline
e_1 & 0 & e_3 & -e_2 \\ \hline
e_2 & -e_3 & 0 & e_1 \\ \hline
e_3 & e_2 & -e_1 & 0
\end{array} 
$$

Putting these together we find:

$$
\begin{array}{c|c|c|c}
 & e_1 & e_2 & e_3 \\ \hline
e_1 & \cdot & \times & \times \\ \hline
e_2 & \times & \cdot & \times \\ \hline
e_3 & \times & \times & \cdot
\end{array} 
$$


## Lagrange's Identity

Earlier we learned that $ \vc{u} \cdot \vc{v} \propto \cos{\theta} $ and $ \vc{u} \times \vc{v} \propto \sin{\theta} $ and this suggests that a pythagorean relation, $ \sin^2 + \cos^2 = 1 $, can be formed between them.

Lagrange's Identity is:

$$
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
= {\lvert \vc{a} \times \vc{b} \rvert}^2 + ( \vc{a} \cdot \vc{b} )^2
$$

It also shows us that the dot and cross products are two parts of a greater whole. It is analogous to Pythagoras Theorem applied to vector multiplication. We can find this using:

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
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - (\vc{a} \cdot \vc{b} )^2 \\
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
&= {\lvert \vc{a} \times \vc{b} \rvert}^2 + ( \vc{a} \cdot \vc{b} )^2
\end{aligned}
$$

Or starting with the dot product:

$$
\begin{aligned}
\vc{a} \cdot \vc{b}
&= \lvert \vc{a} \rvert \lvert\vc{b} \rvert \cos{\theta} \\
{( \vc{a} \cdot \vc{b} )}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 \cos{\theta}^2 \\
{( \vc{a} \cdot \vc{b} )}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 (1 - \sin{\theta}^2) \\
{( \vc{a} \cdot \vc{b} )}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - ({\lvert \vc{a} \rvert} {\lvert\vc{b} \rvert} \sin{\theta} )^2 \\
{( \vc{a} \cdot \vc{b} )}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - \lvert \vc{a} \times \vc{b} \rvert^2 \\
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
&= {\lvert \vc{a} \times \vc{b} \rvert}^2 + ( \vc{a} \cdot \vc{b} )^2
\end{aligned}
$$

