---
title: Morin, Classical Mechanics, Problem 2.13
layout: page
---

# Problem 2.13

## Why this Problem is Cool

1. A good problem to apply linear algebra to

## Problem

We have a horizontal beam supported on each end and a support somewhere in the middle. The mass of the beam, M, is uniformly distributed along it's length. Find an expression for each of the supporting forces. Is it completely solvable?

## Solution

Let $$ F_1 $$, $$ F_2 $$ and $$ F_3 $$ be the upward force at the leftmost, inner and rightmost supports respectively.
Let $$ a $$ be the distance from the leftmost support to the inner support.
Let $$ b $$ be the distance from the inner support to the rightmost support.

We can start by coming up with all the relevant equations by summing the forces to zero and summing the torque/moments to zero.

$$ F_1 + F_2 + F_3 = Mg \tag{1} \label{eq:1} $$

Take the moment around the 1st (leftmost) support assuming positive moment is in the counter-clockwise direction (righthand rule):

$$ aF_2 + (a+b)F_3 = \left( \frac {a+b} {2} \right) Mg \tag{2} \label{eq:2} $$

Take the moment around the 2nd (inner) support:

$$ \begin{align}
-aF_1 + bF_3 &= \left( \frac {a+b} {2} - a \right) Mg = \left( \frac {a-2a+b} {2} \right) Mg \\
-aF_1 + bF_3 &= \left( \frac {b-a} {2} \right) Mg \tag{3} \label{eq:3}  \\
\end{align} $$

Take the moment around the 3rd (rightmost) support:

$$ (a+b)F_1 + bF_2 = \left( \frac {a+b} {2} \right) Mg \tag{4} \label{eq:4} $$

So we have 4 equations and 3 unknowns - seems almost too good to be true. Let's see if it is, by expressing this system of equations in augmented matrix form and then using Gaussian elimination from linear algebra to row reduce.

First, lets make a prediction about how it will turn out. To be held in place, a beam really only needs 2 supports but in our system we have 3. So the 3rd is redundant and could provide anywhere from all or nearly all the support, leaving little to be provided by the other two or it might provide almost no support, in which case the other two must shoulder the load. So we should find that our solution requires one of the supports to provide a fixed amount of support before the support provided by the other two can be determined. For example, if we set one of the supports to provide a force of zero then the weight of the beam should be divided between the other two.

### Gaussian Elimination

$$
\begin{bmatrix}
1 & 1 & 1 &   Mg \\
0 & a & a+b & \left( \frac {a+b} {2} \right) Mg \\
-a & 0 & b &  \left( \frac {b-a} {2} \right) Mg \\
a+b & b & 0 & \left( \frac {a+b} {2} \right) Mg
\end{bmatrix} 
$$

As we consider row reducing in this form, we can see that adding row 2 to row 4 and subtracting row 2 from row 3 gives:

$$
\begin{bmatrix}
1 & 1 & 1       & Mg \\
0 & a & a+b     & \left( \frac {a+b} {2} \right) Mg \\
-a & -a & -a    & -aMg \\
a+b & a+b & a+b & (a+b)Mg
\end{bmatrix} 
$$

It looks like row 4 is just linear combinations of rows 1 and 2. We can zero row 4 out by dividing it by $$ (a+b) $$ and then subtracting row 1. Since we only needed 3 equations for 3 unknowns anyways lets just get rid of this one. Unfortunately, it also looks like row 3 is just a linear combination of rows 1 and 2. We can zero it out by dividing by $$ -a $$ and then subtracting row 1.

$$
\begin{bmatrix}
1 & 1 & 1   & Mg \\
0 & a & a+b & \left( \frac {a+b} {2} \right) Mg \\
0 & 0 & 0   & 0 \\
\end{bmatrix} 
$$

So it's turned out that we really only had 2 equations for our 3 unknowns. We continue reducing by dividing row 2 by a.

$$
\begin{bmatrix}
1 & 1 & 1               & Mg \\
0 & 1 & \frac {a+b} {a} & \left( \frac {a+b} {2a} \right) Mg \\
0 & 0 & 0               & 0 \\
\end{bmatrix} 
$$

Subtracting row 2 from row 1 takes us as far as we can go:

$$
\begin{bmatrix}
1 & 0 & \frac {-b} {a}  & \left( \frac {a-b} {2a} \right) Mg \\
0 & 1 & \frac {a+b} {a} & \left( \frac {a+b} {2a} \right) Mg \\
0 & 0 & 0               & 0 \\
\end{bmatrix} 
$$

So our system is singular and $$ F_3 $$ is a free variable. 
So our solution is going to be parametric in terms of $$ F_3 $$:

$$ \begin{align}
F_1(f) &= \left( \frac {a-b} {a} \right) \frac {Mg} 2 + \frac b a f
  \tag{5} \label{eq:5} \\
F_2(f) &= \left( \frac {a+b} {a} \right) \left( \frac {Mg} 2 - f \right)
  \tag{6} \label{eq:6} \\
F_3(f) &= f
  \tag{7} \label{eq:7} \\
\end{align} $$

So let's play with this a bit. Let's check if our prediction was right and see what happens if the inner support provides no force.

$$ \begin{align}
F_2(f)           &= 0 \\
\left( \frac {a+b} {a} \right) \left( \frac {Mg} 2 - f \right) &= 0 \\
\left( \frac {Mg} 2 - f \right) &= 0 \\
f                &= \frac {Mg} 2
\end{align} $$

Plugging the value of $$ f $$ back in we find:

$$ ( F_1, F_2, F_3) = \left( \frac {Mg} 2, 0, \frac {Mg} 2 \right) $$

Just as we predicted!

What should happen if $$ b = 0 $$ ? $$ F_1 $$ should support the leftmost edge of the beam along with half of it's weight, while $$ F_2 $$ and $$ F_3 $$ should support the rightmost edge and the other half of the beam. Let's see if our solution works out that way...

$$ \begin{align}
F_1(f) &= \left( \frac {a-0} {a} \right) \frac {Mg} 2 + \frac 0 a f = \frac {Mg} 2 \\
F_2(f) &= \left( \frac {a+0} {a} \right) \left( \frac {Mg} 2 - f \right) = \frac {Mg} 2 - f \\
F_3(f) &= f \\
\end{align} $$

Sure enough it does!

### Why did we end up with only 2 equations and 3 unknowns?

We observed during elimination that:
1. equations 1 and 2 could be combined to produce 3
1. equations 1 and 2 could be combined to produce 4

So really, equations 2, 3 and 4 mathematically are different perspectives of the same thing. You can combine equation 1 and any one of the three moment equations to produce the other two. 
