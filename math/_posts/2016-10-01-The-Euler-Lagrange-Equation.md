---
title: The Euler-Lagrange Equation
layout: page
jsarr: scripts/kev-chart.js
---

* This will become a table of contents (this text will be scraped).
{:toc}

# Proof

Our goal, stated in terms of physics/mechanics, is: given a function representing a mechanics problem, and two points representing the start and end position and velocity, we want to find the function $ y(x) $ that would be the only path between the two points the satisfies the laws of physics.

This goal, stated more mathematically, is: given a Lagrangian, $ \mathscr{L} $ which is a function of the function $ y(x) $ that we are looking for, find $ y(x) $ that connects $ (x_1,y_1) $ and $ (x_2, y_2) $ and makes the integral of $ \mathscr{L} $, called the action, a min/max/inflection point. If we succeed, we have found a function that makes the action, $ S $, stationary. Now you might think at first that this is exactly the kind of min/max problem that calculus is good at by taking the derivative and solving it for 0. However, that can only tell us the value of x where there is a minimum. In this case, we're not simply looking for a value of x, we're looking for an entire function!

Here we want to find the function $ y(x) $ that makes the action $ S(x) $ stationary (or in our case, a minimum).

$$ Action = S(x)=\int_{x_1}^{x_2} \mathscr{L}[y(x),y'(x),x]\,dx = \int_{x_1}^{x_2} \mathscr{L}(y,y',x)\,dx $$

In the absence of constraints, many possible functions $ y(x) $ could connect the two points, but to satisfy the laws of physics only a single specific path between the two points is valid. In order to find this path, we need some way to mathematically recognize the difference between a wrong answer and the right one.

$$
\begin{align}
Y(x) &= y(x) + \eta(x) \\
Y'(x) &= y'(x) + \eta'(x)
\end{align}
$$

We do this by introducing a variation from the correct value by adding $ \eta(x) $. In this case, we define $ \eta(x) $ to not be zero, so that adding it to the original will always give a wrong answer. We also need to ensure $ Y(x) $ still connects the two points, so we also add the constraint that $ \eta(x_1) = \eta(x_2) = 0 $.) So, now $ Y(x) $ represents functions that could connect $ (x_1,y_1) $ and $ (x_2, y_2) $ _except_ the one we are really looking for.

In a typical minimization problem, we will need to be able to express varying degrees of correctness/wrongness, so we introduce a scaling factor $ \alpha $:

$$
\begin{align}
Y(\alpha, x) &= y(x) + \alpha\eta(x) \\
Y'(\alpha, x) &= y'(x) + \alpha\eta'(x)
\end{align}
$$

Now the bigger $ \alpha $ is, the more wrong $ Y(x) $ will be and $ Y(x) $ will be the correct answer when $ \alpha = 0 $. We refer to $ \alpha\eta(x) $ as a variation of the minimizing function.  Calculus of Variations owes it's name to this idea.

So we can rewrite our original problem in terms of our new function as:

$$ S(\alpha, x) = \int_{x_1}^{x_2} \mathscr{L}(Y(\alpha, x), Y(\alpha, x)', x)\ dx $$

Since S is a function of $ \alpha $ now, the original problem of finding the function that makes the integral of S stationary, has become a vanilla "find the local minimum" calculus problem where we set the derivative to zero. We now also require that $ \alpha = 0 $.

Restating in mathematical notation, we want to solve this equation for the action $ S $:

$$ \left. \frac{\partial S(\alpha)}{\partial \alpha}\ \right |_{\alpha = 0} = 0 $$

noting that we must use a partial derivative because $ L $ is a function of both $ x $ and $ \alpha $.

Expressing $ S $ in terms of $ Y $ we find:

$$ \frac{\partial}{\partial \alpha}\ \left[\int_{x_1}^{x_2} L(Y, Y', x)\ dx\right]
= \int_{x_1}^{x_2} \frac {\partial L} {\partial \alpha}\,dx = 0
$$

Now we can solve the partial derivative, and to do this we will need to apply the chain rule which takes the form:

$$
\begin{align}
\frac {\partial} {\partial \alpha} L(Y(\alpha, x),Y'(\alpha, x), x)
&= \frac {dY} {d\alpha} \ \frac {\partial L} {\partial Y} + \frac {dY'} {d\alpha}\ \frac {\partial L} {\partial Y'} + \frac {dx} {d\alpha} \ \frac {\partial L} {\partial x} \\[10pt]
&= \eta\frac {\partial L} {\partial Y} + \eta'\frac {\partial L} {\partial Y'}
\end{align}
$$

Plugging this back in, we get:

$$
\left. \frac {\partial S} {\partial \alpha}\ \right |_{\alpha = 0}
= \int_{x_1}^{x_2} \left(  \eta\frac {\partial L} {\partial Y}+\eta'\frac {\partial L} {\partial Y'} \right)\,dx = 0
$$

At this point, $ \eta $ appears twice and we could gather them if one was not a derivative. We can fix this by taking advantage of the following property of integration by parts:

$ \int u dv = uv - \int v du $, notice how $ udv $ and $ vdu $ switch places?

We can now write:

$$
\begin{align}
&= \int_{x_1}^{x_2} \eta\frac {\partial L} {\partial Y}\,dx + \int_{x_1}^{x_2} \eta'\frac {\partial L} {\partial Y'}\,dx \\[10pt]
&= \int_{x_1}^{x_2} \eta\frac {\partial L} {\partial Y}\,dx - \int_{x_1}^{x_2} \eta \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right)\,dx + \left[ \eta \frac {\partial L} {\partial y'} \right]_{x_1}^{x_2} \\[10pt]
&= \int_{x_1}^{x_2} \eta \left[ \frac {\partial L} {\partial Y} - \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right) \right] \,dx + \left[ \eta \frac {\partial L} {\partial y'} \right]_{x_1}^{x_2}
\end{align}
$$

The last term evaluates to zero because we had to define $ \eta $ at the beginning so that $ \eta(x_1) = \eta(x_2) = 0 $, and so we have:

$$
\left. \frac {\partial S} {\partial \alpha}\ \right |_{\alpha = 0}
= \int_{x_1}^{x_2} \eta \left[ \frac {\partial L} {\partial Y} - \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right) \right] \,dx = 0
$$

Above we defined $ \eta $ to be a non-zero function, in order for the integral to evaluate to zero, it must be the case that:

$$
\left[ \frac {\partial L} {\partial Y} - \frac {d} {dx} \left( \frac {\partial L} {\partial Y'} \right) \right]_{\alpha = 0} = 0
$$

Because $ \alpha = 0 $, we find that $ (Y, Y') = (y, y') $ and so:

$$
\boxed {\frac {\partial L} {\partial y} - \frac {d} {dx} \left( \frac {\partial L} {\partial y'} \right) = 0}
$$

This is the Euler-Lagrange equation.

# TODO:

1. Motivating example.
* Shortest distance between two points on a plane?
* Shortest distance between two points on a sphere?
1. What is the difference between the Calculus of Variations and Principle of Stationary Action?
1. What does "stationary" actually mean?

Applications of the calculus of variations include:

* Variational method (quantum mechanics), one way of finding approximations to the lowest energy eigenstate or ground state, and some excited states;
* Variational Bayesian methods, a family of techniques for approximating intractable integrals arising in Bayesian inference and machine learning.
* Variational methods in general relativity, a family of techniques using calculus of variations to solve problems in Einstein's theory of general relativity.
* Finite element method is a variational method for finding approximate solutions to boundary value problems in differential equations.


# D3 Graph

Example

<style>

body {
  width: 960px;
  height: 500px;
  position: relative;
}

.axis path,
.axis line {
  fill: none;
  stroke: white;
  shape-rendering: crispEdges;
}

.axis text {
  font: 10px sans-serif;
  stroke: white;
}

.line {
  fill: none;
  stroke-linecap: round;
  stroke: white;
}

line {
  stroke: white;
  shape-rendering: crispEdges;
}

form {
  position: absolute;
  bottom: 27px;
  right: 50px;
}

input {
  width: 140px;
}

output {
  display: inline-block;
  width: 3.5em;
}

</style>


<div id="kdgform">
  <div id="acceleration">
    <input type="range" min="0" max="1" step=".01" value=".55">
    <span><i>a</i> = <output name="acceleration"></output></span>
  </div>
  <div id="reflection">
    <input type="range" min="0" max="1" step=".01" value=".5">
    <span><i>r</i> = <output name="reflection"></output></span>
  </div>
</div>

# References
TODO:

* Taylor
* Morin
* Mathematics of Technology
* wikipedia
* [Edwin Taylor](http://www.eftaylor.com/leastaction.html)
