---
title: Vector Dot Product
layout: page
---
$$
\newcommand\ihat{\hat{\boldsymbol{\imath}}}
\newcommand\jhat{\hat{\boldsymbol{\jmath}}}
\newcommand\khat{\hat{\boldsymbol{k}}}
\newcommand\vc[1]{\mathbf{#1}}
\newcommand\inner[2]{ \langle {#1}, {#2} \rangle }
\newcommand\abs[2]{ \lvert {#1} \rvert }
$$

* This will become a table of contents (this text will be scraped).
{:toc}

# Dot Product

A dot product takes two vectors and produces a number that represents the degree to which the two vectors point in the same direction. The closer they are to pointing in the same direction, the larger the result will be and if they are not parallel at all, then the result will be 0. So what does all this have to do with multiplication? When the dot product is largest because the vectors are both pointing in the same direction, the result is the two lengths multiplied together. So the dot product combines both multiplying the vector lengths with measuring how parallel the vectors are.

Since it produces a number, it is sometimes referred to as the Scalar Product.

# Dot Product Emergence

The dot product relation emerges naturally from Pythagoras' theorem. To see this happen, we will explore perpendicular vectors, which have the special property of having a dot product of zero.

Consider vectors $ \vc{a} $ and $ \vc{b} $ where $ \vc{a} $ is perpendicular to $ \vc{b} $. We can think of them as the opposite and adjacent sides of a right triangle and therefore, apply Pythagoras.

When $ \vc{a} \perp \vc{b} $:

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

Now lets consider what we have here. We have found a function of two vectors $ f(\vc{a}, \vc{b}) = a_x b_x + a_y b_y + a_z b_z $ that is zero when the vectors are perpendicular.

This is exactly the same as the dot product which is 0 when the vectors are perpendicular:

$$ \vc{a} \cdot \vc{b} = a_x b_x + a_y b_y + a_z b_z $$


## Definition

We will define the dot product in two different ways. Once from the perspective of geometry, where a vector has a length and a direction and the other from the perspective of algebra where a vector is comprised of coordinates. Let's start with the geometric viewpoint:

__Geometric Definition:__ $ \vc{u} \cdot \vc{v} = \lvert u \rvert \lvert v \rvert \cos {\theta} $  

A way to think of this is the dot product multiplies the lengths of two vectors _but only the parts that lie in the same direction_ and that is what the $ \cos{\theta} $ term is for.

We will explore what this means in detail but for now just play around with the example by dragging the vectors around and observing that effect of making the vectors longer, shorter, more parallel and more perpendicular have on the dot product.

Notice also that if the vectors are 1 dimensional, then the dot product simplifies to the usual multiplying two numbers together.

<script>  
    var ggbApp = new GGBApplet({"appName": "geometry", "material_id":"e5hhjxct", "width": 300, "height": 250, "allowStyleBar": false, "showToolBar": false, "showAlgebraInput": false, "showMenuBar": false }, true);
    window.addEventListener("load", function() { 
        ggbApp.inject('ggb-DotProduct');
    });
</script>
<div id="ggb-DotProduct"></div> 

### Geometric Intuition #1: the Angle between Two Vectors

One way to think of the dot product is through it's ability to determine the angle between two vectors. The angle should be independent of whatever lengths the two vectors may have so we can write:

$$ \hat{a} \cdot \hat{b} = \cos{\theta} $$

If we now substitute

$$ \hat{a} = \frac{\vc{a}}{\lvert a \rvert} \;\;\; \hat{b} = \frac{\vc{b}}{\lvert b \rvert} $$

we get the original definition:

$$ \vc{a} \cdot \vc{b} = \lvert a \rvert \lvert b \rvert \cos {\theta} $$  

### Geometric Intuition #2: Parallel and Perpendicular Vectors

We can develop our intuition by trying the dot product out with some simple parallel and perpendicular vectors, $ \ihat $ and $ \jhat $ the x and y axis unit vectors.

$$
\begin{aligned}
\ihat \cdot \ihat &= (1)(1) \cos 0 = 1  \\
\ihat \cdot \jhat &= (1)(1) \cos 90^\circ = 0 \\
\jhat \cdot \jhat &= (1)(1) \cos 0 = 1
\end{aligned}
$$

As expected, we find:

$$
\begin{aligned}
\vc{u} \cdot \vc{v} &= 0 \text{, when } \vc{u} \perp \vc{v} \\
\vc{u} \cdot \vc{v} &= \lvert\vc{u}\rvert \lvert\vc{v}\rvert \text{, when } \vc{u} \parallel \vc{v}
\end{aligned}
$$

So the dot product can be a handy way to find out if two vectors are perpendicular or not. If dotting them produces 0 then they are perpendicular. You can also use this to find a line that is perpendicular to the one you have. The dot product of the vector you have and the one you're looking for will be 0.

### Geometric Intuition #3: Projections

Next lets see what happens when we dot a regular vector, $ \vc{u} = ( r, \angle \theta) $, with these same unit vectors.

$$
\begin{aligned}
u_x = \vc{u} \cdot \ihat &= r (1) \cos{\theta} &= r \cos \theta \\
u_y = \vc{u} \cdot \jhat &= r (1) \cos{(90^\circ - \theta)} &= r \sin \theta
\end{aligned}
$$

Here we find that the dot product has given us the scalar projection/component of the vector $ \vc{u} $ onto the x and y axis respectively, something done frequently in engineering and physics.

We can take this further and find the vector projection (aka vector component) in the direction of any vector using, for example, $ \vc{u_v} $ the projection of $ \vc{u} $ in the direction of $ \vc{v} $:

$$ u_v =
\vc{u} \cdot \hat{v} =
\vc{u} \cdot \frac{\vc{v}}{\lvert v \rvert} =
\frac{\vc{u} \cdot \vc{v}}{\lvert v \rvert}
$$

$$ \vc{u_v}
= u_v \hat{v}
= ( \vc{u} \cdot \hat{v} ) \hat{v}
= \frac{\vc{u} \cdot \vc{v}}{\lvert v \rvert} \frac{\vc{v}}{\lvert v \rvert}
= \frac{\vc{u} \cdot \vc{v}}{\lvert v \rvert^2} \vc{v}
$$

### Geometric Intuition #4: Projection + Multiplication

Now we are in a position to put this all together. If instead of a unit vector we used a second regular vector, we would still have the $ r \cos \theta $ part but instead of (1) for the unit vector we will have the length of the second vector. It's saying take all of the second vector and multiply it by the amount of the first vector that lies in the same direction. Conversely you could think of the projection being from the second onto the first. It's symmetric so it doesn't matter.

### Dot Product using Coordinates

__Algebraic Definition:__ $ \vc{u} \cdot \vc{v} = u_x v_x + u_y v_y + u_z v_z $

Remember that the dot product multiplies two vectors _but only the parts that lie in the same direction_, when dealing with coordinates, this is accomplished by multiplying like components together.

Now lets look at how the algebraic definition can be derived. We already know that the dot product has the following properties:

>Left Distributive over vector addition: $ \vc{a} \cdot (\vc{b} + \vc{c} ) = \vc{a} \cdot \vc{b} + \vc{a} \cdot \vc{c} $  
Right Distributive over vector addition: $ (\vc{a} + \vc{b}) \cdot \vc{c} = \vc{a} \cdot \vc{c} + \vc{b} \cdot \vc {c} $  
Scalar multiplication:  $ (c_{1}\vc {a} )\cdot (c_{2}\vc {b} )=c_{1}c_{2}(\vc {a} \cdot \vc {b} ) $  
And, as we found, above: $ \ihat \cdot \ihat = \jhat \cdot \jhat = \khat \cdot \khat = 1 $ and $ \ihat \cdot \jhat = \ihat \cdot \khat = \jhat \cdot \khat = 0 $

Here we write $ \vc{u} $ and $ \vc{v} $ as a linear combination of the standard $ \mathbb{R}^3 $ unit vectors:

$$
\begin{aligned}
\vc{u} &= u_x \ihat + u_y \jhat + u_z \khat \\
\vc{v} &=  v_x \ihat + v_y \jhat + v_z \khat
\end{aligned}
$$

Now we can write out the dot product of these two vectors, and by applying the above properties, we can multiply it all out:

$$
\begin{aligned}
\vc{u} \cdot \vc{v}
= \; &\begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix} \cdot
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix} \\
= \; &u_x \ihat \cdot v_x \ihat + u_x \ihat \cdot v_y \jhat + u_x \ihat \cdot v_z \khat + \\
&u_y \jhat \cdot v_x \ihat + u_y \jhat \cdot v_y \jhat + u_y \jhat \cdot v_z \khat + \\
&u_z \khat \cdot v_x \ihat + u_z \khat \cdot v_y \jhat + u_z \khat \cdot v_z \khat \\
= \;&
u_x v_x \underbrace{\ihat \cdot \ihat}_{=1} +
u_x v_y \underbrace{\ihat \cdot \jhat}_{=0} +
u_x v_z \underbrace{\ihat \cdot \khat}_{=0} +\\
&u_y v_x \jhat \cdot \ihat + u_y v_y \underbrace{\jhat \cdot \jhat}_{=1} + u_y v_z \jhat \cdot \khat +\\
&u_z v_x \khat \cdot \ihat + u_z v_y \khat \cdot \jhat + u_z v_z \underbrace{\khat \cdot \khat}_{=1}
\end{aligned}
$$

Therefore most of the terms cancel and we are left with what we stated as Definition #2 above:

$$ \vc{u} \cdot \vc{v} = u_x v_x + u_y v_y + u_z v_z $$

This component-based description is interesting because it really makes clear that only like components of the two vectors are being multiplied.

Now lets see what happens when we dot a vector, $ \vc{u} = \langle u_x, u_y, u_z \rangle $ with the standard unit vectors in $\mathbb{R}^3$.

$$
\begin{aligned}
\vc{u} \cdot \ihat
= \langle u_x, u_y, u_z \rangle \cdot \langle 1, 0, 0 \rangle
= \langle u_x, 0, 0 \rangle \\
\vc{u} \cdot \jhat
= \langle u_x, u_y, u_z \rangle \cdot \langle 0, 1, 0 \rangle
= \langle 0, u_y, 0 \rangle \\
\vc{u} \cdot \khat
= \langle u_x, u_y, u_z \rangle \cdot \langle 0, 0, 1 \rangle
= \langle 0, 0, u_z \rangle
\end{aligned}
$$

Again we find that the dot product is a useful tool for finding the projection of a vector in the direction of a unit vector.

## Applications

The angle between two vectors is found by knowing that the cosine of the angle between them is their dot product divided by their self dot product.

In physics, you’re often interested in knowing to what extent a vector quantity contributes in a given direction (the vector quantity’s component in that direction). This is what the dot (scalar) product tells you.

In physics, the work expression is $ W = \vec{F} \cdot \vec{r} $. Only the force component parallel to the direction (or likewise, the position component parallel to the force) is wanted.

# The Inner and Outer Products

The dot product is very useful in $ \mathbb{R}^3 $ but also very specific to $ \mathbb{R}^3 $. Since goal of linear algebra is to apply to vectors of any kind, whether they be audio data, polynomials, etc., the inner product takes the idea of a dot product and makes it more general and abstract so that it can apply to any kind of vector. The inner product of two vectors is shown as $ \langle \vc{a}, \vc{b} \rangle $. The inner product is defined as any operator that adheres to the following properties:

>Commutative: $ \inner{\vc a}{\vc b}  = \inner{\vc b}{\vc a} $  
>Scalar Mult: $ \alpha \inner{\vc a}{\vc b}  = \inner{\alpha \vc a}{\vc b} $  
>Distributive: $ \inner{\vc{a}}{\vc{b}+\vc{c}} = \langle \vc{a}, \vc{b} \rangle + \langle \vc{a}, \vc{c} \rangle $  
>Positive Definite $ \inner{\vc v}{\vc v} \ge 0 $ and equal iff $ \vc v= 0 $

We can also write the dot product, aka inner product, as the following matrix multiplication:

$$
\begin{aligned}
\text{inner product} = \vc{u} \cdot \vc{v} = \vc{u}^\intercal \vc{v}
&= \begin{bmatrix}
u_x \\
u_y \\
u_z \\
\end{bmatrix}^\intercal
\begin{bmatrix}
v_x \\
v_y \\
v_z \\
\end{bmatrix} \\
&= \begin{bmatrix} u_x & u_y & u_z \end{bmatrix}
\begin{bmatrix} v_x \\ v_y \\ v_z \end{bmatrix}
= u_x v_x + u_y v_y + u_z v_z \\
\text{outer product} = \vc{u} \otimes \vc{v}
= \vc{u} \vc{v}^\intercal
&= \begin{bmatrix}
u_x \\
u_y \\
u_z \\
\end{bmatrix}
\begin{bmatrix}
v_x \\
v_y \\
v_z \\
\end{bmatrix}^\intercal \\
\end{aligned}
$$

Notice that for the inner product, the transpose is on the inner vector and for the outer product, the transpose is on the outer most vector.

TODO
