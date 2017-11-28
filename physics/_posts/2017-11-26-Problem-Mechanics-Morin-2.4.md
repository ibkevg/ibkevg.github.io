---
title: Morin, Classical Mechanics, Problem 2.4
layout: page
---

# Problem 2.4

A block of mass $$ M $$ is positioned against a vertical wall. The coeffient of friction between the block and the wall is $$ \mu $$. You wish to keep the block from falling by pushing on it with a force of $$ F $$ at an angle $$ \theta $$ wrt horizontal ($$ -\frac \pi 2 \lt \theta \lt \frac \pi 2 $$).

<div style="text-align:center;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.4-a.svg" type="image/svg+xml" align="center"/>
</div>

(a) What's the minimum force required to prevent the block from falling for any given angle $$ \theta $$?

(b) At what angle $$ \theta $$ is the minimum force smallest? And what is the corresponding force?

(c) What is the limiting value of $$ \theta $$ below which there does not exist an $$ F $$ that keeps the block up?

# Solution

TODO: insert free body diagram here

## Minimum Force
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

Find $$ \frac {dF} {d\theta} = 0 $$

$$ \begin{align}

\frac {dF} {d\theta} &= gM \frac {d} {d\theta} \left( \mu \cos \theta + \sin \theta \right) ^{-1} \\

&= -gM ( \mu \cos \theta + \sin \theta)^{-2} (-\mu \sin \theta + \cos \theta) \\

&= -\mu \sin \theta + \cos \theta \\

\end{align} $$

Setting the derivative to zero we find:

$$
\begin{align}

-\mu \sin \theta + \cos \theta &= 0 \\
\mu \sin \theta &= \cos \theta \\

\frac {\sin \theta} {\cos \theta} &= \frac 1 \mu \\

\theta &= \tan^{-1} \frac 1 \mu \\

\end{align}
$$

Now we substitute this value for $$ \theta $$ back into $$ F(\theta) $$

$$ F \geq \frac {gM} {\mu \cos \left( \tan^{-1} \frac 1 \mu \right) + \sin \left(\tan^{-1} \frac 1 \mu \right) } $$

To simplify we would like to find a way to change $$ \cos ( \tan^{-1} ) $$ into $$ \cos ( \cos^{-1} ) $$ because  $$ \cos ( \cos^{-1} \theta) = \theta $$. Since $$ \tan \theta = \frac 1 \mu $$, we know the opposite and adjacent sides and can relate the hypotenuse, $$ h^2 = 1^2 + \mu^2 $$. With that, we can re-express $$ \theta $$ in terms of $$ \cos $$ and $$ \sin $$.

<div style="text-align:center;">
<embed src="{{ site.url }}{{ site.baseurl }}/assets/svg/Mechanics-Morin-2.4-c.svg" type="image/svg+xml" align="center"/>
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

