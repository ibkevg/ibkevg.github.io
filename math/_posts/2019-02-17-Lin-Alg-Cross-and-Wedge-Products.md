---
title: Vector Cross Product
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

# Cross Product

http://en.wikipedia.org/wiki/Cross_product#History


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


## Cross Product vs Determinant

TODO


# The Wedge Product

You might think of the wedge product as analagous to the cross product but in a way that isn't limited to 3 dimensions like the cross product is. This is sometimes referred to as the exterior product.

$$ \vc{a} \times \vc{b} \text{ ... analagous to ... } \vc{a} \wedge \vc{b} $$

TODO

