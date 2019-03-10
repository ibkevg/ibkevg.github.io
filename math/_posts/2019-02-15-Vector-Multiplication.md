---
title: Vector Multiplication
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

# Introduction

There are lots of ways to multiply vectors

| *Notation* | *Description* | *Produces ...* |  
| $$ a \vc{u} $$ | scalar multiplication| vector |  
| $$ \vc{u} \cdot \vc{v} $$ | dot product (aka scalar product) | scalar |  
| $$ \vc{u} \times \vc{v} $$ | cross product | vector |  
| $$ \inner{\vc u}{\vc v} $$ | inner product (~= dot product) | scalar |  
| $$ \vc{u} \wedge \vc{v} $$ | wedge product (aka exterior product) | bivector |  
| $$ \vc{u}\vc{v} = \vc{u} \cdot \vc{v} + \vc{u} \wedge \vc{v} $$ | geometric product | multivector |  
| $$ \vc{u} \otimes \vc{v} $$ | outer product (aka tensor product) | tensor, multilinear matrix |  

My goal here is to:

1. show what these vector operations do
1. help build intuition about what they really mean
1. provide examples of how to use them
1. show why the vector products took the form that they do and not some other form

# Scalar Multiplication

Multiplying a vector by a scalar produces another vector.

$$
\vc{u}
= a \vc{v}
= a \begin{bmatrix} v_x \\ v_y \end{bmatrix} = \begin{bmatrix} a v_x \\ a v_y \end{bmatrix}
$$

Much of the intuition from multipling two scalars applies when multiplying a vector by a scalar: If we multiply a vector by 1, it stays exactly the same. If we multiply a vector by 2, it becomes twice as long. If we multiply by 1/2, it shrinks in half. Also, the scalar's sign affects the vector direction: if we multiply a vector by -1, it stays the same length but reverses direction. 

<script>  
    var ggbApp2 = new GGBApplet({"appName": "geometry", "material_id":"jh2hvwhs", "width": 400, "height": 175, "allowStyleBar": false, "showToolBar": false, "showAlgebraInput": false, "showMenuBar": false }, true);
    window.addEventListener("load", function() { 
        ggbApp2.inject('ggb-ScalarMultiplication');
    });
</script>
<div id="ggb-ScalarMultiplication"></div>

## The Null or Zero Vector

If we multiply a vector by zero, we get a null vector aka a zero vector, $$\vc{0}$$.

$$ 0 \vc{v} = \vc{0} $$

That doesn't seem particularly startling because after all anything times 0 is 0, right? So lets explore what this means in terms of rectangular coordinates and then geometrically.

$$
0 \vc{v} 
= 0 \begin{bmatrix} v_x \\ v_y \end{bmatrix}
= \begin{bmatrix} 0v_x \\ 0v_y \end{bmatrix}
= \begin{bmatrix} 0 \\ 0 \end{bmatrix}
$$

Here we find that a Null vector has no direction at all because there's no way to measure the angle between two lines of 0 length. It's like asking what is the angle of a plate of spaghetti? It's a question that doesn't have a meaningful answer.

Now how should we think of this in geometry, length and angle, terms? It makes sense that $$ \vc{v} $$'s length becomes zero, but what happens to it's direction?

$$ 0 \vc{v} = 0 \langle r, \angle{\theta } \rangle = \langle 0, \angle{???} \rangle $$

We could think of a null vector as pointing in any direction because all vectors, of all directions, shrink in the limit down to a null vector:

$$ \lim_{r \to 0} \langle r, \angle{\theta } \rangle = \vc{0} $$

But then what angle should the zero vector have here:

$$ \vc{a} + (-\vc{a}) = \vc{0} $$

So the reality is a direction is only meaningful when accompanied by a non-zero length. It might seem contradictory to say that a null vector is both "any direction" and "no particular direction" but these are really just different ways to express in english that it is mathematically undefined.

So for $$\vc{0}$$, the length is zero, and the direction is undefined.

## Unit Vectors

Scalar multiplication is also useful for creating and using unit vectors.

A unit vector is a handy way to represent a direction without a specific magnitude. Notationally, we write it with a hat, for example, $$ \hat{\vc{a}} $$ is a unit vector in the direction of $$ \vc{a} $$.

You might think that for a vector to represent a direction alone it should have no notion of length at all, i.e. if the vector is $$ \langle r, \angle{\theta} \rangle $$, it's corresponding unit vector might be just the angle. But as we just learned, a vector with no length is a zero vector, $$ \vc{0}, $$ and a zero vector's direction is undefined. So, for a vector to have a direction it must also have a length. Having "unit" in the name gives us a hint as to what it's length is because unit means 1 and that is the length of a unit vector.

The reason unit vectors are so handy is because anything times 1 is itself, thus unit vectors can be multiplied by any scalar to create vectors of any length you need. As an example, we can make a $$ \vc{b} $$ in the direction of $$ \hat{\vc{a}} $$ using $$ \vc{b} = 5 \hat{\vc{a}} $$. So, $$ \vc{b} $$ has length, $$ \lvert\vc{b}\rvert = 5 $$.

To make $$ \hat{\vc{a}} $$, we take vector $$ \vc{a} $$ and divide out it's length, $$ \lvert\vc{a}\rvert $$, in effect normalizing it's components to 1.

$$ \hat{\vc{u}} = \frac{\vc{u}}{\lvert\vc{u}\rvert} $$

where a vector's length is:

$$ \lvert\vc{u}\rvert = \sqrt{u_x^2 + u_y^2 + u_z^2} $$

To recreate the original vector we combine the two using the following scalar multiplication:

$$ \vc{u} = \lvert\vc{u}\rvert \hat{u} $$

Unit vectors have many uses, for example, $$ \mathbb{R}^3 $$ has standard unit vectors that form the foundation of the (x, y, z) coordinate system:

$$
\begin{aligned}
\ihat &= (1,0,0) \\
\jhat &= (0,1,0) \\
\khat &= (0,0,1) \\
\end{aligned}
$$

Any vector in $$ \mathbb{R}^3 $$ can be written as a linear combination of these standard unit vectors:

$$ \vc{u} = u_x \ihat + u_y \jhat + u_z \khat $$

# Vector to Vector Products

| $$ \vc{a} \cdot \vc{b} $$ |dot product  |  the dot product of two vectors provides a measure of how parallel the vectors are |  
| $$ \vc{a} \times \vc{b} $$ |cross product | the cross product of two vectors provides a measure of how perpendicular the vectors are|

 Vector to vector products can be tricky to understand at first because it's not obvious how we should extend our experience multiplying two numbers together to account for the directionality that vectors have. So before we introduce the equations that define dot and cross products, lets check if the dot and cross products have, at their core, the ordinary multiplication of vector lengths as you might expect.

To do this, let's express our vectors as the product of a length and a unit vector and then track how each part influences $$ \vc{a} \cdot \vc{b} $$ and $$ \vc{a} \times \vc{b} $$.

$$ \vc{a} = \lvert\vc{a}\rvert \hat{a} $$

$$ \vc{b} = \lvert\vc{b}\rvert \hat{b} $$

>Note: we also need to know how the dot and cross products behave under scalar multiplication. For now, please accept that the following properties are true:  
>$$ (c \vc{a}) \cdot \vc{b} = \vc{a} \cdot (c \vc{b}) = c (\vc{a} \cdot \vc{b}) $$  
>$$ (c \vc{a}) \times \vc{b} = \vc{a} \times (c \vc{b}) = c (\vc{a} \times \vc{b}) $$

Working this out, we can see that indeed both vector products begin by multiplying the vector lengths together:

$$
\begin{aligned}
\vc{a} \cdot \vc{b} = (\lvert\vc{a} \rvert \hat{a}) \cdot (\lvert\vc{b} \rvert \hat{b})
&= \lvert \vc{a} \rvert \lvert \vc{b} \rvert (\hat{a} \cdot \hat{b})\\
\vc{a} \times \vc{b} = (\lvert\vc{a} \rvert \hat{a}) \times (\lvert\vc{b} \rvert \hat{b})
&= \lvert \vc{a} \rvert \lvert \vc{b} \rvert (\hat{a} \times \hat{b})
\end{aligned}
$$

and where the magic happens is how the dot and cross products vary in how they account for the vector directions.



# Dot Product

A dot product takes two vectors and produces a number that represents the degree to which the two vectors point in the same direction. The closer they are to pointing in the same direction, the larger the result will be and if they are not parallel at all, then the result will be 0. So what does all this have to do with multiplication? When the dot product is largest because the vectors are both pointing in the same direction, the result is the two lengths multiplied together. So the dot product combines both multiplying the vector lengths with measuring how parallel the vectors are.

Since it produces a number, it is sometimes referred to as the Scalar Prodcut.

## Definition

We will define the dot product in two different ways. Once from the perspective of geometry, where a vector has a length and a direction and the other from the perspective of algebra and coordinates. Let's start with the geometric viewpoint:

__Definition #1, The Geometric Viewpoint:__ $$ \vc{u} \cdot \vc{v} = \lvert u \rvert \lvert v \rvert \cos {\theta} $$  

A way to think of this is the dot product multiplies the lengths of two vectors _but only the parts that lie in the same direction_ and that is what the $$ \cos{\theta} $$ term is for.

We will explore what this means in detail but for now just play around with the example by dragging the vectors around and observing that effect of making the vectors longer, shorter, more parallel and more perpendicular have on the dot product.

Notice also that if the vectors are 1 dimensional, then the dot product simplifies to the usual multiplying two numbers together.

<script>  
    var ggbApp = new GGBApplet({"appName": "geometry", "material_id":"e5hhjxct", "width": 300, "height": 250, "allowStyleBar": false, "showToolBar": false, "showAlgebraInput": false, "showMenuBar": false }, true);
    window.addEventListener("load", function() { 
        ggbApp.inject('ggb-DotProduct');
    });
</script>
<div id="ggb-DotProduct"></div> 

### Geometric Interpretation #1: the Angle between Two Vectors

Another way to think of the dot product is as a means of determining the angle between two vectors. The angle should be independent of whatever lengths the two vectors may have so we can write:

$$ \hat{a} \cdot \hat{b} = \cos{\theta} $$

If we now substitute $$ \hat{a} = \frac{\vc{a}}{\lvert a \rvert} $$ we get the original definition:

$$ \vc{a} \cdot \vc{b} = \lvert a \rvert \lvert b \rvert \cos {\theta} $$  

Now to develop our intuition, let's first try this out with some simple vectors, $$ \ihat $$ and $$ \jhat $$ the x and y axis unit vectors.

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

So the dot product can be a handy way to find out if two vectors are perpendicular or not. If dotting them produces 0 then they are perpendicular. Another way this can be useful is if you want to find a line that is perpendicular to the one you have.

### Geometric Interpretation #2: Projection

Next lets see what happens when we dot a regular vector, $$ \vc{u} = ( r, \angle \theta) $$, with these same unit vectors.

$$
\begin{aligned}
u_x = \vc{u} \cdot \ihat &= r (1) \cos{\theta} &= r \cos \theta \\
u_y = \vc{u} \cdot \jhat &= r (1) \cos{(90^\circ - \theta)} &= r \sin \theta
\end{aligned}
$$

Here we find that the dot product has given us the scalar projection/component of the vector $$ \vc{u} $$ onto the x and y axis respectively, something done frequently in engineering and physics.

We can take this further and find the vector projection (aka vector component) in the direction of any vector using, for example, $$ \vc{u_v} $$ the projection of $$ \vc{u} $$ in the direction of $$ \vc{v} $$:

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

### Geometric Interpretation #3: Projection + Multiplication

Now we are in a position to put this all together. If instead of a unit vector we used a second regular vector, we would still have the $$ r \cos \theta $$ part but instead of (1) for the unit vector we will have the length of the second vector. It's saying take all of the second vector and multiply it by the amount of the first vector that lies in the same direction. Conversely you could think of the projection being from the second onto the first. It's symmetric so it doesn't matter.

### Dot Product using Coordinates

__Definition #2, The Coordinate Viewpoint:__ $$ \vc{u} \cdot \vc{v} = u_x v_x + u_y v_y + u_z v_z $$

Remember that the dot product multiplies two vectors _but only the parts that lie in the same direction_, when dealing with coordinates, this is accomplished by multiplying like components together.

Now lets look at how the coordinate oriented definition #2 can be derived from definition #1. Here we write $$ \vc{u} $$ and $$ \vc{v} $$ as a linear combination of the standard $$ \mathbb{R}^3 $$ unit vectors:

$$
\begin{aligned}
\vc{u} &= u_x \ihat + u_y \jhat + u_z \khat \\
\vc{v} &=  v_x \ihat + v_y \jhat + v_z \khat
\end{aligned}
$$

Now we can write out the dot product as:

$$ \vc{u} \cdot \vc{v}
= \begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix} \cdot
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix}
$$

Now we can multiply it all out because the dot product has the following properties:

>Left Distributive over vector addition: $$ \vc{a} \cdot (\vc{b} + \vc{c} ) = \vc{a} \cdot \vc{b} + \vc{a} \cdot \vc{c} $$  
Right Distributive over vector addition: $$ (\vc{a} + \vc{b}) \cdot \vc{c} = \vc{a} \cdot \vc{c} + \vc{b} \cdot \vc {c} $$  
Scalar multiplication:  $$ (c_{1}\vc {a} )\cdot (c_{2}\vc {b} )=c_{1}c_{2}(\vc {a} \cdot \vc {b} ) $$  
And we found above: $$ \ihat \cdot \ihat = \jhat \cdot \jhat = \khat \cdot \khat = 1 $$ and $$ \ihat \cdot \jhat = \ihat \cdot \khat = \jhat \cdot \khat = 0 $$

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

This component-based description is interesting in the sense that it's kind of like regular 1 dimensional multiplication except you multiply only the parts of the vector that are in the same direction.

Now lets see what happens when we dot a vector, $$ \vc{u} = (u_x, u_y, u_z) $$ with the standard unit vectors in $$\mathbb{R}^3$$.

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

# The Inner and Outer Products

The dot product is very useful in $$ \mathbb{R}^3 $$ but also very specific to $$ \mathbb{R}^3 $$. Since goal of linear algebra is to apply to vectors of any kind, whether they be audio data, polynomials, etc., the inner product takes the idea of a dot product and makes it more general and abstract so that it can apply to any kind of vector. The inner product of two vectors is shown as $$ \langle \vc{a}, \vc{b} \rangle $$. The inner product is defined as any operator that adheres to the following properties:

>Commutative: $$ \inner{\vc a}{\vc b}  = \inner{\vc b}{\vc a} $$  
>Scalar Mult: $$ \alpha \inner{\vc a}{\vc b}  = \inner{\alpha \vc a}{\vc b} $$  
>Distributive: $$ \inner{\vc{a}}{\vc{b}+\vc{c}} = \langle \vc{a}, \vc{b} \rangle + \langle \vc{a}, \vc{c} \rangle $$  
>Positive Definite $$ \inner{\vc v}{\vc v} \ge 0 $$ and equal iff $$ \vc v= 0 $$

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

# Cross Product

TODO

# Lagrange's Identity

Lagrange's Identity shows us that the dot and cross products are two parts of a greater whole. It is analogous to Pythagoras Theorem but for vector multiplication.

$$ \boxed{
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
= {\lvert \vc{a} \times \vc{b} \rvert}^2 + \lvert \vc{a} \cdot \vc{b} \rvert^2
} $$

We can find this using:

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
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - \lvert \vc{a} \cdot \vc{b} \rvert^2 \\
\end{aligned}
$$

# Dot and Cross Product Emergence from Pythagoras' Theorem

The dot and cross products emerge naturally from Pythagoras' theorem. To see how this works, below we will take advantage of the fact that the dot product of two perpendicular vectors is zero and the cross product of two parallel vectos is zero.

## Emergence of the Dot Product from Pythagoras' Theorem

We first consider the case where $$ \vc{a} $$ is perpendicular to $$ \vc{b} $$. When $$ \vc{a} \perp \vc{b} $$, they form the opposite and adjacent sides of a right triangle, so we can apply Pythagoras to get:

$$
\begin{aligned}
|\vc{s}|^2_{perp}
&=  \lvert \vc{a} \rvert^2  +  \lvert \vc{b} \rvert^2 \\
|\vc{s}|^2_{perp}
&=  (a_x^2 + a_y^2 + a_z^2)  +  (b_x^2 + b_y^2 + b_z^2)
\end{aligned}
$$

Also, regardless of perpendicularity, the difference between any $$ \vc{a} $$ and $$ \vc{b} $$ is $$ \vc{s} = \vc{a} - \vc{b} $$, therefore:

$$ |\vc{s}|^2 = (a_x-b_x)^2 + (a_y-b_y)^2 + (a_z-b_z)^2 $$

Now when $$ \vc{a} \perp \vc{b} $$, we can equate $$ \abs{\vc{s}}^2 = \abs{\vc{s}}^2_{perp} $$ and cancel terms to arrive at:

$$ a_x b_x + a_y b_y + a_z b_z =  0 $$

This is consistent with the definition of the dot product:

$$ \vc{a} \cdot \vc{b} = a_x b_x + a_y b_y + a_z b_z $$

## Emergence of the Cross Product from Pythagoras' Theorem

Now let's consider the case where $$ \vc{a} $$ is parallel to $$ \vc{b} $$. We can't directly apply Pythagoras but we can apply the law of cosines:

$$ |\vc{s}|^2 = |\vc{a}|^2 + |\vc{b}|^2 - 2|\vc{a}||\vc{b}|\cos S $$

and because our vectors are parallel, $$ S = 180^\circ $$ making $$ \cos 180^\circ = -1 $$, which gives:

$$
\begin{aligned}
|\vc{s}|^2_{parallel}
&=  |\vc{a}|^2 + |\vc{b}|^2 + 2|\vc{a}||\vc{b}| \\
&=  (a_x^2 + a_y^2 + a_z^2)  +  (b_x^2 + b_y^2 + b_z^2) + 2|\vc{a}||\vc{b}|
\end{aligned}
$$

Also, regardless of parallelity, the sum of any $$ \vc{a} $$ and $$ \vc{b} $$ is $$ \vc{s} = \vc{a} + \vc{b} $$, therefore:

$$ |\vc{s}|^2 = (a_x + b_x)^2 + (a_y + b_y)^2 + (a_z + b_z)^2 $$

Now when $$ \vc{a} \parallel \vc{b} $$, $$ \abs{\vc{s}}^2 = \abs{\vc{s}}^2_{parallel} $$, so we can equate these two expressions, and cancel terms to arrive at:

$$
\begin{aligned}
a_x b_x + a_y b_y + a_z b_z &=  \sqrt{a_x^2 + a_y^2 + a_z^2}\sqrt{b_x^2 + b_y^2 + b_z^2} \\
(a_x b_x + a_y b_y + a_z b_z)^2 &=  (a_x^2 + a_y^2 + a_z^2)(b_x^2 + b_y^2 + b_z^2) \\
\end{aligned}
$$

Expanding these expressions and cancelling terms, we get:

$$
2a_x b_x a_y b_y + 2a_x b_x a_z b_z + 2a_y b_y a_z b_z
= (a_x b_y)^2 + (a_x b_z)^2 + (a_y b_x)^2 + (a_y b_z)^2 + (a_z b_x)^2 + (a_z b_y)^2
$$

Notice that we can gather terms and re-write this equality as

$$ (a_x b_y - b_x a_y)^2  +  (b_x a_z - a_x b_z)^2  +  (a_y b_z - b_y a_z)^2  =  0 $$

This sum of squares equals zero only when $$ \vc{a} \parallel \vc{b} $$ and is consistent with the definition of the cross product:

$$ \vc{a} \times \vc{b}
= \begin{bmatrix}
a_y b_z - b_y a_z \\
a_y b_z - b_y a_z \\
a_x b_y - b_x a_y
\end{bmatrix}
$$

Also as we saw previously, the dot product of two vectors is 0 if the vectors are perpendicular, so we can confirm that $$ \vc{a} \times \vc{b} $$ is perpendicular to both of them.

We find that $$ \vc{a} \cdot (\vc{a} \times \vc{b}) $$  is zero:

$$ a_x a_y b_z - a_x b_y a_z  +  a_y b_x a_z - a_y a_x b_z  +  a_z a_x b_y - a_z b_x a_y  =  0 $$

and likewise $$ \vc{b} \cdot (\vc{a} \times \vc{b}) $$  is zero:

$$ b_x a_y b_z - b_x b_y a_z  +  b_y b_x a_z - b_y a_x b_z  +  b_z a_x b_y - b_z b_x a_y  =  0 $$


# The Wedge Product

You might think of the wedge product as analagous to the cross product but in a way that isn't limited to 3 dimensions like the cross product is. This is sometimes referred to as the exterior product.

$$ \vc{a} \times \vc{b} \text{ ... analagous to ... } \vc{a} \wedge \vc{b} $$

TODO

# Geometric Algebra

The big idea of geometric algebra (aka Clifford Algebra) is to explicitly define vector multiplication in the following way:

$$ \vc{a} \vc{b} = \vc{a} \cdot \vc{b} + \vc{a} \wedge \vc{b} $$

TODO


# References to incorporate

Was linear algebra discovered or invented?
https://www.quora.com/Was-mathematics-invented-or-discovered-1


When we talk about a product in mathematics, we generally want the product to have a few features, similar to multiplication among numbers:
https://www.quora.com/Why-is-the-dot-product-of-two-vectors-a-scalar-number

Dividing with Vectors
https://physics.stackexchange.com/questions/14082/what-is-the-physical-significance-of-dot-cross-product-of-vectors-why-is-divi

Why does vector multiply require both dot and exterior product?
https://physics.stackexchange.com/questions/186045/why-do-we-need-both-dot-product-and-cross-product

Some good PDFs
http://www.math.ucla.edu/~josephbreen/Understanding_the_Dot_Product_and_the_Cross_Product.pdf
https://math.la.asu.edu/~surgent/mat272/dotcross.pdf
