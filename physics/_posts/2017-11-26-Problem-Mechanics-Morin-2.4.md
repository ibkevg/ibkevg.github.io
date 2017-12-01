---
title: Morin, Classical Mechanics, Problem 2.4
layout: page
---

# Problem 2.4

A block of mass $$ M $$ is positioned against a vertical wall. The coeffient of friction between the block and the wall is $$ \mu $$. You wish to keep the block from falling by pushing on it with a force of $$ F $$ at an angle $$ \theta $$ wrt horizontal ($$ -\frac \pi 2 \lt \theta \lt \frac \pi 2 $$).

<div style="text-align:center;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.4-a.svg" type="image/svg+xml"/>
</div>

(a) What's the minimum force required to prevent the block from falling for any given angle $$ \theta $$?

(b) At what angle $$ \theta $$ is the minimum force smallest? And what is the corresponding force?

(c) What is the limiting value of $$ \theta $$ below which there does not exist an $$ F $$ that keeps the block up?

# Solution

## Minimum Force

We start by drawing the free body diagram:

<div style="text-align:left;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.4-b.svg" type="image/svg+xml"/>
</div>

We choose the sign for the static friction force to oppose gravity, since our goal is for the combination of the friction and our applied force to counter the block's own weight.

$$ \begin{align}
\sum F_y = 0 &= \mu N + F \sin \theta - gM \tag{1} \label{eq:1} \\
\sum F_x = 0 &= F \cos \theta - N \\
N &= F \cos \theta \tag{2} \label{eq:2} \\
\end{align} $$

Substituting $$ \eqref{eq:2} $$ in $$ \eqref{eq:1} $$, we find:

$$ F (\mu \cos \theta + \sin \theta) = gM $$

$$ F \geq \frac {gM} {\mu \cos \theta + \sin \theta} $$

We call this the minimum force because static friction is able to resist higher forces too.

## Angle $$ \theta $$ of the smallest force?
This is the classic use for a derivative where we look for a minimum, which is when the rate of change equals zero. Strictly speaking we would need to confirm we did indeed find a minimum and not a max or point of inflection.

So our goal is to find $$ \frac {dF} {d\theta} = 0 $$

$$ \begin{align}

\frac {dF} {d\theta} &= gM \frac {d} {d\theta} \left( \mu \cos \theta + \sin \theta \right) ^{-1} \\

&= -gM ( \mu \cos \theta + \sin \theta)^{-2} (-\mu \sin \theta + \cos \theta) \\

&= gM \frac {(\mu \sin \theta - \cos \theta)} {( \mu \cos \theta + \sin \theta)^2} \\

\end{align} $$

We can now solve this for 0. Observe that the numerator of the fraction is what can make this equation zero, so we can divide out/ignore the denominator. Also we can ignore/divide out the $$ gM $$ term because our block can never be massless. So we are left with:

$$
\begin{align}
\mu \sin \theta - \cos \theta &= 0 \\
\mu \sin \theta &= \cos \theta \\

\frac {\sin \theta} {\cos \theta} &= \frac 1 \mu \\

\theta &= \tan^{-1} \frac 1 \mu \\

\end{align}
$$

Now we substitute this value for $$ \theta $$ back into $$ F(\theta) $$

$$ F \geq \frac {gM} {\mu \cos \left( \tan^{-1} \frac 1 \mu \right) + \sin \left(\tan^{-1} \frac 1 \mu \right) } $$

To simplify we would like to find a way to change $$ \cos ( \tan^{-1} ) $$ into $$ \cos ( \cos^{-1} ) $$ because  $$ \cos ( \cos^{-1} \theta) = \theta $$. Since $$ \tan \theta = \frac 1 \mu $$, we know the opposite and adjacent sides and can relate the hypotenuse, $$ h^2 = 1^2 + \mu^2 $$. With that, we can re-express $$ \theta $$ in terms of $$ \cos $$ and $$ \sin $$.

<div style="text-align:center;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.4-c.svg" type="image/svg+xml"/>
</div>

So, we get $$ \cos \theta = \frac \mu {\sqrt {1 + \mu^2}} $$ and $$ \sin \theta = \frac 1 {\sqrt{1 + \mu^2}} $$ which can now use to simplify $$ F $$:

$$
\begin{align}

F &\geq \frac {gM} {\mu \cos \left( \cos^{-1} \frac \mu {\sqrt{1 + \mu^2}} \right) + \sin \left(\sin^{-1} \frac 1 {\sqrt{1 + \mu^2}} \right) } \\

F &\geq \frac {gM} {\mu \left( \frac \mu {\sqrt{1 + \mu^2}} \right) + \left( \frac 1 {\sqrt{1 + \mu^2}} \right) } \\

F &\geq \frac {gM} {\left( \frac {1 + \mu^2} {\sqrt{1 + \mu^2}} \right)} \\

F &\geq \frac {gM} {\sqrt{1 + \mu^2}}
\end{align}
$$

## Limiting value of $$ \theta $$

Given that: $$ F \geq \frac {gM} {\mu \cos \theta + \sin \theta} $$, we can see that $$ F $$ has no solution when

$$ \mu \cos \theta + \sin \theta \leq 0 $$

$$ \frac {\sin \theta} {\cos \theta} = -\mu $$

$$ \theta = \tan^{-1} -\mu $$

