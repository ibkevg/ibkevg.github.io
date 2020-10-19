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

Big Picture

If we multiply vectors, we should be able to produce a result in every direction.
If we construct a multiplication table for every basis vector.







Here we compare the multiplication tables for the dot and wedge products and find that they each address orthogonal parts, suggesting that the two may be combined.

We will then find equations that allow us to determine if two vectors are parallel or perpendicular. Although we start only with the basic laws of triangles like Pythagorus and the law of cosines, we will find that the equations for the dot and wedge products emerge.

Finally we will look at Lagrange's Identity that further points in this direction.

# Multiplication Tables

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
e_1 & dot & cross & cross \\ \hline
e_2 & cross & dot & cross \\ \hline
e_3 & cross & cross & dot
\end{array} 
$$

## Lagrange's Identity

Earlier we learned that $ \hat{u} \cdot \hat{v} = \cos{\theta} $ and $ \hat{u} \times \hat{v} = \sin{\theta} $ and this suggests that a pythagorean relation, $ \sin^2 + \cos^2 = 1 $, can be formed between them.

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

