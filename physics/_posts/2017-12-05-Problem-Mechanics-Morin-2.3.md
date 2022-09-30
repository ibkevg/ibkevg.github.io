---
title: Morin, Classical Mechanics, Problem 2.3
layout: page
---

# Problem 2.3

## Why this Problem is Cool

It's kind of like problem 2.1 but in multiple dimensions

## Question

A frictionless tube lies in the vertical plane and is in the shape of a function that has its endpoints at the same height but is otherwise arbitrary. A chain with uniform mass per unit length lies in the tube from end to end. Show, by considering the net force of gravity along the curve, that the chain doesn't move.

<div style="text-align:center;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.3-a.svg" type="image/svg+xml"/>
</div>

## Solution

Let's define $ f(x) $ to describe the curvature of the tube and therefore, the chain inside it. We also note that the endpoints have the same height, so:

$$ f(a) = f(b) \tag{1} \label{eq:1} $$

Similar to what we did for Problem 2.1, lets start by drawing a free body diagram for an infinitesimally short section of chain, $ ds $, along the curving tube.

<div style="text-align:center;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.3-c.svg" type="image/svg+xml"/>
</div>

The mass of chain section $ ds $ is $ dm = \rho ds $ and so the force due to gravity is:

$$ dF_g = g dm = g \rho ds  \tag{2} \label{eq:2} $$

By definition the normal force, $ dF_n = \cos \theta dF_g $, cannot contribute to motion of the chain lengthwise along the tube, so we don't need to analyze it. The tangential force however, equation $ \eqref{eq:3} $, points along the length of the tube.

$$ \begin{align}
dF_t &= \sin \theta dF_g \tag{3} \label{eq:3} \\
     &= \sin \theta g \rho ds \\
\end{align} $$


We have this force in terms of $ \theta $ but we need it to be in terms of $ f(x) $, the function that describes the shape of the tube/chain. We do this by considering the geometry of $ ds $.

<div style="text-align:center;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.3-b.svg" type="image/svg+xml"/>
</div>

$$ ds = \sqrt { {dx}^2 + (f'dx)^2} = \sqrt { 1 + f'(x)^2} dx  \tag{4} \label{eq:4} $$

$$ \sin \theta = \frac {f'(x) dx} {ds}= \frac {f'(x) dx} {\sqrt {1+f'(x)^2} dx} = \frac {f'(x)} {\sqrt {1+f'(x)^2}} \tag{5} \label{eq:5} $$

Now we can take $ \eqref{eq:3} $ and substitute $ \sin \theta $ from $ \eqref{eq:5} $ and $ ds $ from $ \eqref{eq:4} $ to get:

$$ \begin{align}
dF_t &=  g \rho \frac {f'(x)} {\sqrt {1+f'(x)^2}} \sqrt { 1 + f'(x)^2} dx \\
dF_t &=  g \rho f'(x) dx \\
\end{align} $$

Now we integrate this force from end to end along the chain, to find out the net force:

$$ \begin{align}
\int dF_t &= \rho g \int_a^b f'(x) dx \\
F_t &= \rho g [f(b) - f(a)] \tag{6} \label{eq:6} \\
\end{align} $$

 Now remember the problem constraint, $ \eqref{eq:3} $, that states the the two endpoints have the same height. This means $ f(b) - f(a) = 0 $ and thus:

 $$ F_t = 0 $$

 A net force of 0 indicates that the chain is static.

## Relationship with Problem 2.1

Since we didn't specify the actual shape of the tube or chain, we can play with this now and see how our result holds up if we envision the chain was completely vertical as is the case in problem 2.1.

$ f(a) = 0 $ and $ f(b) = h $, where h = the height of the chain.

By substituting these into $ \eqref{eq:6} $ we find:

$$ F_t = \rho g [f(b) - f(a)] = g \rho (h - 0) = \rho gh$$

The chain will fall unless we hold it in place, exactly the value we came up with in Problem 2.1