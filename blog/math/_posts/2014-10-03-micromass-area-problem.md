---
title: Micromass Physics Forum October Challenge
image: assets/images/NASA/ISS-Moonset.jpg 
layout: post
---


![Problem]( {{ site.baseurl }}/assets/images/micromass-area-problem.jpg)

Strategy: We can take advantage of the symmetry of the diagram, to simplify the problem. We can take right half of the diagram, rotate it counter clockwise by 180 degrees and overlay it ontop of the left half of the diagram. In doing this, we find that the top 2 corners and the lower right corners are completely filled with red. The remaining corner is partially filled in and for it, we can determine the area that's red by subtracting the amount that's white from the area of the entire corner. We will call this area that's white, W. It is the area under two intervals, first the line and then the curve. 

We start by defining the line and the circle.

For the circle, $$ r = 5 $$, and $$ center = (5,5) $$

$$ r^2 = x^2 + y^2 $$

$$ r^2 = (x - 5)^2 + (y - 5)^2 $$

$$
\begin{align}
y &= 5 + \sqrt {r^2 - (x - 5)^2} \\[5pt]
 &= 5 + \sqrt {25 - (x^2 - 10x + 25)} \\[5pt]
 &= 5 + \sqrt {x(10 - x)}
\end{align}
$$

For the line, with points at $$ (0,0) $$ and $$ (10, 5) $$

$$ y= \frac {1} {2} x $$


To determine the white area, W, we want to find the following definite integral:

$$ W = \int_0^\alpha \frac {1} {2} x\ dx + \int_\alpha^5 5 + \sqrt {x(10 - x)}\ dx $$

where $$ \alpha $$ is the intersection of the line and the circle.

To find $$ \alpha $$:

$$
\begin{align}
\frac {1} {2} x &= 5 + \sqrt {x(10 - x)} \\[5pt]
\left( \frac {1} {2} x - 5\right)^2 &= x(10 - x) \\[5pt]
\frac {1} {4} x^2 - 5x + 25 &= 10x - x^2 \\[5pt]
\frac {5} {4} x^2 - 15x + 25 &= 0 \\[5pt]
\frac {1} {4} x^2 - 3x + 5 &= 0
\end{align}
$$

Using the quadratic formula, we find $$ \alpha = x = 2 $$.

We can now return to the equation for W:

$$ W = \int_0^2 \frac {1} {2} x\ dx + \int_2^5 5 + \sqrt {x(10 - x)}\ dx $$

$$ W = \left[\frac {1} {4} x^2 \right]_0^2 + \left[5x\right]_0^2  + \int_2^5 \sqrt {x(10 - x)}\ dx $$

$$ W = 11 + \int_2^5 \sqrt {x(10 - x)}\ dx $$

