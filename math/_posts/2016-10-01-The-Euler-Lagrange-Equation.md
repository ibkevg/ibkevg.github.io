---
title: The Euler-Lagrange Equation
image: assets/images/NASA/Pluto-Haze.jpg
layout: post
---

* This will become a table of contents (this text will be scraped).
{:toc}

TODO:

1. Motivating example.
* Shortest distance between two points on a plane?
* Shortest distance between two points on a sphere?
1. What is the difference between the Calculus of Variations and Principle of Stationary Action?
1. What does "stationary" actually mean?

Applications of the calculus of variations include:

Variational method (quantum mechanics), one way of finding approximations to the lowest energy eigenstate or ground state, and some excited states;

Variational Bayesian methods, a family of techniques for approximating intractable integrals arising in Bayesian inference and machine learning.

Variational methods in general relativity, a family of techniques using calculus of variations to solve problems in Einstein's theory of general relativity.

Finite element method is a variational method for finding approximate solutions to boundary value problems in differential equations.

# References
TODO:
* Taylor
* Morin
* Mathematics of Technology
* wikipedia

# Proof

$$ S(x)=\int_{x_1}^{x_2} L[y(x),y'(x),x]\,dx $$

We're looking for the function $$ y(x) $$ that connects $$ (x_1,y_1) $$ and $$ (x_2, y_2) $$ and makes the integral of S a min/max/inflection point. Another way to say this is that we're looking for a function that makes S stationary.

To start, let's simplify our notation a bit:

$$ S(x) = \int_{x_1}^{x_2} L(y,y',x)\,dx $$

The answer we're looking for, $$ y(x) $$, is a specific path - the min/max/saddlepoint - between the two points. Any other path is wrong. In order to find this path, we need some way to describe how close a solution is getting to the correct one. So we next explore a modified $$ y(x) $$ that is guaranteed to produce the wrong path between the points:

$$
\begin{align}
Y(x) &= y(x) + \eta(x) \\
Y'(x) &= y'(x) + \eta'(x)
\end{align}
$$

Here we've introduced this "wrongness" by adding $$ \eta(x). $$ There are infinitely many choices for the $$ \eta(x) $$ function and when added to $$ y(x) $$ they all give the wrong answer. (Note that to ensure $$ Y $$ still connects the two points, there is the constraint that $$ \eta(x_1) = \eta(x_2) = 0 $$.)

If $$ \eta(x) $$ was zero on the interval $$ [x_1, x_2] $$, then $$Y(x)$$ would be the same as $$y(x)$$, making it the function we're looking for. However, $$ \eta(x) $$ is not zero, it's any one of an infinite set of functions that when added to $$ y(x) $$ make it wrong. We can "fix" this with a small tweak:

$$
\begin{align}
Y(\alpha, x) &= y(x) + \alpha\eta(x) \\
Y'(\alpha, x) &= y'(x) + \alpha\eta'(x)
\end{align}
$$

Now $$ Y(x) $$ will be the correct answer when $$ \alpha = 0 $$ and the bigger $$ \alpha $$ is, the more wrong $$ Y(x) $$ will be. We refer to $$ \alpha\eta(x) $$ as a variation of the minimizing function.  Calculus of Variations owes it's name to this idea.

So we can rewrite our original problem as:

$$
\begin{align}
S(\alpha) &= \int_{x_1}^{x_2} L(y+\alpha\eta, y'+\alpha\eta', x)\,dx \\[10pt]
&= \int_{x_1}^{x_2} f(Y, Y', x)\ dx
\end{align}
$$

Since S is a function of $$ \alpha $$ now, the original problem, of finding the function that makes the integral of S stationary, has become a vanilla "find the local minimum" calculus problem where we set the derivative to zero. We now also require that $$ \alpha = 0 $$.

Restating in mathematical notation, we want to solve this equation:

$$ \left. \frac{\partial S(\alpha)}{\partial \alpha}\ \right |_{\alpha = 0} = 0 $$

which becomes:

$$ \frac{\partial}{\partial \alpha}\ \left[\int_{x_1}^{x_2} L(Y, Y', x)\ dx\right]
= \int_{x_1}^{x_2} \frac {\partial L} {\partial \alpha}\,dx = 0
$$

Note that must use a partial derivative because $$ L $$ is a function of both $$ x $$ and $$ \alpha $$. In order to determine the partial derivative, we will need to apply the chain rule which takes the form:

$$
\begin{align}
\frac {\partial} {\partial \alpha} L(Y(\alpha, x),Y'(\alpha, x), x)
&= \frac {dY} {d\alpha} \ \frac {\partial L} {\partial Y}
 + \frac {dY'} {d\alpha}\ \frac {\partial L} {\partial Y'}
 + \frac {dx} {d\alpha} \ \frac {\partial L} {\partial x}\\[10pt]
&= \eta\frac {\partial L} {\partial Y} + \eta'\frac {\partial L} {\partial Y'}
\end{align}
$$

Plugging this back in, we get:

$$
\left. \frac {\partial S} {\partial \alpha}\ \right |_{\alpha = 0}
= \int_{x_1}^{x_2} \left(  \eta\frac {\partial L} {\partial Y}+\eta'\frac {\partial L} {\partial Y'} \right)\,dx = 0
$$

At this point, $$ \eta $$ appears twice and we could gather them if one was not a derivative. We can fix this by taking advantage of the following property of integration by parts:

$$ \int u dv = uv - \int v du $$, notice how $$ udv $$ and $$ vdu $$ switch places?

We can now write:

$$
\begin{align}
&= \int_{x_1}^{x_2} \eta\frac {\partial L} {\partial Y}\,dx
+ \int_{x_1}^{x_2} \eta'\frac {\partial L} {\partial Y'}\,dx \\[10pt]

&= \int_{x_1}^{x_2} \eta\frac {\partial L} {\partial Y}\,dx
- \int_{x_1}^{x_2} \eta \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right)\,dx
+ \left[ \eta \frac {\partial L} {\partial y'} \right]_{x_1}^{x_2} \\[10pt]

&= \int_{x_1}^{x_2} \eta \left[ \frac {\partial L} {\partial Y} - \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right) \right] \,dx
+ \left[ \eta \frac {\partial L} {\partial y'} \right]_{x_1}^{x_2}
\end{align}
$$

The last term evaluates to zero because we had to define $$ \eta $$ at the beginning so that $$ \eta(x_1) = \eta(x_2) = 0 $$, and so we have:

$$
\left. \frac {\partial S} {\partial \alpha}\ \right |_{\alpha = 0}
= \int_{x_1}^{x_2} \eta \left[ \frac {\partial L} {\partial Y} - \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right) \right] \,dx = 0
$$

Above we defined $$ \eta $$ to be a non-zero function, in order for the integral to evaluate to zero, it must be the case that:

$$
\left[ \frac {\partial L} {\partial Y} - \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right) \right]_{\alpha = 0} = 0
$$

Because $$ \alpha = 0 $$, we find that $$ (Y, Y') = (y, y') $$ and so:

$$
\boxed {\frac {\partial L} {\partial y} - \frac {d} {dx} \left( \frac {\partial L} {\partial y'} \right) = 0}
$$


