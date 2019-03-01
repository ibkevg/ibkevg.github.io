---
title: Vector Multiplication
layout: page
---
$$
\newcommand{\ihat}{\hat{\boldsymbol{\imath}}}
\newcommand{\jhat}{\hat{\boldsymbol{\jmath}}}
\newcommand{\khat}{\hat{\boldsymbol{k}}}
$$

* This will become a table of contents (this text will be scraped).
{:toc}

# Introduction

There are several ways to multiply vectors and here we will be talking about three of them.

| $$ a \vec{u} $$ | scalar multiplication | scalar to vector | produces a vector |  
| $$ \vec{u} \cdot \vec{v} $$ | dot product (aka scalar product) | vector to vector | produces a scalar |  
| $$ \vec{u} \times \vec{v} $$ | cross product | vector to vector | produces a vector |

My goal here is to:

1. show what these vector operations do
1. help build intuition about what they really mean
1. provide examples of how to use them
1. show why the vector products took the form that they do and not some other form

# Scalar Multiplication

Multiplying a vector by a scalar produces another vector.

$$
\vec{u}
= a \vec{v}
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

If we multiply a vector by zero, we get the null vector aka the zero vector, $$\vec{0}$$. That doesn't seem particularly startling because after all anything times 0 is 0, right? Except... we're dealing with vectors now, it makes sense that $$ \vec{v} $$'s length becomes zero, but what happens to it's direction?

$$
\begin{aligned}
\vec{u}
&= 0 \vec{v} = \vec{0} \\
&= 0 \begin{bmatrix} v_x \\ v_y \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}
\end{aligned}
$$

There are several ways to look at this. One is that it has no direction at all. The direction a vector points in is the triangle formed by the vector's length, drawn tip to tail, and a reference line, say the X axis. If the length is 0 we have no line to measure an angle from. It's a point in space rather than a line and a point can't have an angle.

Another, opposite, way to look at this is that the null vector is pointing in all directions at once because all vectors of all directions, shrink in the limit down to the null vector:

$$ \lim_{r \to 0} \langle r, \angle{\theta } \rangle = \vec{0} $$

It might seem contradictory to say that the null vector is both "every direction" and "no particular direction" but these are really just different english expressions for the same mathematical concept.

So for $$\vec{0}$$, the length is zero, but the direction is arbitrary.

## Unit Vectors

Scalar multiplication is also handy for creating and using unit vectors. A unit vector represents a direction and we write it with a hat. For example, $$ \hat{a} $$ is a unit vector in the direction of $$ \vec{a} $$. Having "unit" in the name gives us a hint as to what it's length is because unit means 1 and that is the length of a unit vector. You can multiply a vector whose length is 1 by any scalar length to create vectors of any length you need.

You might think that for a vector to represent a direction alone it should have no notion of length at all, i.e. if the vector is $$ \langle r, \angle{\theta} \rangle $$, it's corresponding unit vector might be just the angle. But as we just learned, a vector with no length is the zero vector, $$ \vec{0} $$ and the zero vector has no particular direction. So, for a vector to have a direction it must also have a length.

As an example, we can make a $$ \vec{b} $$ in the direction of $$ \hat{a} $$ using $$ \vec{b} = 5 \hat{a} $$. So, $$ \vec{b} $$ has length, $$ \lvert\vec{b}\rvert = 5 $$.

To make $$ \hat{a} $$, we take vector $$ \vec{a} $$ and divide out it's length, $$ \lvert\vec{u}\rvert $$, in effect normalizing it to 1.

$$ \hat{u} = \frac{\vec{u}}{\lvert\vec{u}\rvert} $$

where a vector's length is:

$$ \lvert\vec{u}\rvert = \sqrt{u_x^2 + u_y^2 + u_z^2} $$

To recreate the original vector we combine the two using the following scalar multiplication:

$$ \vec{u} = \lvert\vec{u}\rvert \hat{u} $$

Unit vectors have many uses, for example, $$ \mathbb{R}^3 $$ has standard unit vectors that form the foundation of the (x, y, z) coordinate system:

$$
\begin{aligned}
\ihat &= (1,0,0) \\
\jhat &= (0,1,0) \\
\khat &= (0,0,1) \\
\end{aligned}
$$

Any vector in $$ \mathbb{R}^3 $$ can be written as a linear combination of these standard unit vectors:

$$ \vec{u} = u_x \ihat + u_y \jhat + u_z \khat $$

# Vector to Vector Products

| $$ \vec{a} \cdot \vec{b} $$ |dot product  |  the dot product of two vectors provides a measure of how parallel the vectors are |  
| $$ \vec{a} \times \vec{b} $$ |cross product | the cross product of two vectors provides a measure of how perpendicular the vectors are|

 Vector to vector products can be tricky to understand at first because it's not obvious how we should extend our experience multiplying two numbers together to account for the directionality that vectors have. So before we introduce the equations that define dot and cross products, lets check if the dot and cross products have, at their core, the ordinary multiplication of vector lengths as you might expect.

To do this, let's express our vectors as the product of a length and a unit vector and then track how each part influences $$ \vec{a} \cdot \vec{b} $$ and $$ \vec{a} \times \vec{b} $$.

$$ \vec{a} = \lvert\vec{a}\rvert \hat{a} $$

$$ \vec{b} = \lvert\vec{b}\rvert \hat{b} $$

>Note: we also need to know how the dot and cross products behave under scalar multiplication. For now, please accept that the following properties are true:  
>$$ (c \vec{a}) \cdot \vec{b} = \vec{a} \cdot (c \vec{b}) = c (\vec{a} \cdot \vec{b}) $$  
>$$ (c \vec{a}) \times \vec{b} = \vec{a} \times (c \vec{b}) = c (\vec{a} \times \vec{b}) $$

Working this out, we can see that indeed both vector products begin by multiplying the vector lengths together:

$$
\begin{aligned}
\vec{a} \cdot \vec{b} = (\lvert\vec{a} \rvert \hat{a}) \cdot (\lvert\vec{b} \rvert \hat{b})
&= \lvert \vec{a} \rvert \lvert \vec{b} \rvert (\hat{a} \cdot \hat{b})\\
\vec{a} \times \vec{b} = (\lvert\vec{a} \rvert \hat{a}) \times (\lvert\vec{b} \rvert \hat{b})
&= \lvert \vec{a} \rvert \lvert \vec{b} \rvert (\hat{a} \times \hat{b})
\end{aligned}
$$

and where the magic happens is how the dot and cross products vary in how they account for the vector directions.

# Dot Product

A dot product takes two vectors and produces a number that represents the degree to which the two vectors point in the same direction. The closer they are to pointing in the same direction, the larger the result will be and if they are not parallel at all, then the result will be 0. So what does all this have to do with multiplication? When the dot product is largest because the vectors are both pointing in the same direction, the result is the two lengths multiplied together. So the dot product combines both multiplying the vector lengths with measuring how parallel the vectors are.

Since it produces a number, it is sometimes referred to as the Scalar Prodcut.

## Definition

We will define the dot product in two different ways. Once from the perspective of geometry, where a vector has a length and a direction and the other from the perspective of algebra and coordinates. Let's start with the geometric viewpoint:

__Definition #1, The Geometric Viewpoint:__ $$ \vec{u} \cdot \vec{v} = \lvert u \rvert \lvert v \rvert \cos {\theta} $$  

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

If we now substitute $$ \hat{a} = \frac{\vec{a}}{\lvert a \rvert} $$ we get the original definition:

$$ \vec{a} \cdot \vec{b} = \lvert a \rvert \lvert b \rvert \cos {\theta} $$  

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
\vec{u} \cdot \vec{v} &= 0 \text{, when } \vec{u} \perp \vec{v} \\
\vec{u} \cdot \vec{v} &= \lvert\vec{u}\rvert \lvert\vec{v}\rvert \text{, when } \vec{u} \parallel \vec{v}
\end{aligned}
$$

So the dot product can be a handy way to find out if two vectors are perpendicular or not. If dotting them produces 0 then they are perpendicular. Another way this can be useful is if you want to find a line that is perpendicular to the one you have.

### Geometric Interpretation #2: Projection

Next lets see what happens when we dot a regular vector, $$ \vec{u} = ( r, \angle \theta) $$, with these same unit vectors.

$$
\begin{aligned}
u_x = \vec{u} \cdot \ihat &= r (1) \cos{\theta} &= r \cos \theta \\
u_y = \vec{u} \cdot \jhat &= r (1) \cos{(90^\circ - \theta)} &= r \sin \theta
\end{aligned}
$$

Here we find that the dot product has given us the scalar projection/component of the vector $$ \vec{u} $$ onto the x and y axis respectively, something done frequently in engineering and physics.

We can take this further and find the vector projection (aka vector component) in the direction of any vector using, for example, $$ \vec{u_v} $$ the projection of $$ \vec{u} $$ in the direction of $$ \vec{v} $$:

$$ u_v =
\vec{u} \cdot \hat{v} =
\vec{u} \cdot \frac{\vec{v}}{\lvert v \rvert} =
\frac{\vec{u} \cdot \vec{v}}{\lvert v \rvert}
$$

$$ \vec{u_v}
= u_v \hat{v}
= ( \vec{u} \cdot \hat{v} ) \hat{v}
= \frac{\vec{u} \cdot \vec{v}}{\lvert v \rvert} \frac{\vec{v}}{\lvert v \rvert}
= \frac{\vec{u} \cdot \vec{v}}{\lvert v \rvert^2} \vec{v}
$$

### Geometric Interpretation #3: Projection + Multiplication

Now we are in a position to put this all together. If instead of a unit vector we used a second regular vector, we would still have the $$ r \cos \theta $$ part but instead of (1) for the unit vector we will have the length of the second vector. It's saying take all of the second vector and multiply it by the amount of the first vector that lies in the same direction. Conversely you could think of the projection being from the second onto the first. It's symmetric so it doesn't matter.

### Dot Product using Coordinates

__Definition #2, The Coordinate Viewpoint:__ $$ \vec{u} \cdot \vec{v} = u_x v_x + u_y v_y + u_z v_z $$

Remember that the dot product multiplies two vectors _but only the parts that lie in the same direction_, when dealing with coordinates, this is accomplished by multiplying like components together.

Now lets look at how the coordinate oriented definition #2 can be derived from definition #1. Here we write $$ \vec{u} $$ and $$ \vec{v} $$ as a linear combination of the standard $$ \mathbb{R}^3 $$ unit vectors:

$$
\begin{aligned}
\vec{u} &= u_x \ihat + u_y \jhat + u_z \khat \\
\vec{v} &=  v_x \ihat + v_y \jhat + v_z \khat
\end{aligned}
$$

Now we can write out the dot product as:

$$ \vec{u} \cdot \vec{v}
= \begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix} \cdot
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix}
$$

Now we can multiply it all out because the dot product has the following properties:

>Left Distributive over vector addition: $$ \vec{a} \cdot (\vec{b} + \vec{c} ) = \vec{a} \cdot \vec{b} + \vec{a} \cdot \vec{c} $$  
Right Distributive over vector addition: $$ (\vec{a} + \vec{b}) \cdot \vec{c} = \vec{a} \cdot \vec{c} + \vec{b} \cdot \vec {c} $$  
Scalar multiplication:  $$ (c_{1}\vec {a} )\cdot (c_{2}\vec {b} )=c_{1}c_{2}(\vec {a} \cdot \vec {b} ) $$

$$
\begin{aligned}
\vec{u} \cdot \vec{v}
= \; &\begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix} \cdot
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix} \\
= \; &u_x \ihat \cdot v_x \ihat + u_x \ihat \cdot v_y \jhat + u_x \ihat \cdot v_z \khat + \\
&u_y \jhat \cdot v_x \ihat + u_y \jhat \cdot v_y \jhat + u_y \jhat \cdot v_z \khat + \\
&u_z \khat \cdot v_x \ihat + u_z \khat \cdot v_y \jhat + u_z \khat \cdot v_z \khat \\
= \; &u_x v_x \ihat \cdot \ihat + u_x v_y \ihat \cdot \jhat + u_x v_z \ihat \cdot \khat +\\
&u_y v_x \jhat \cdot \ihat + u_y v_y \jhat \cdot \jhat + u_y v_z \jhat \cdot \khat +\\
&u_z v_x \khat \cdot \ihat + u_z v_y \khat \cdot \jhat + u_z v_z \khat \cdot \khat
\end{aligned}
$$

Remember that above we found:

$$ \ihat \cdot \ihat = \jhat \cdot \jhat = \khat \cdot \khat = 1 $$
$$ \ihat \cdot \jhat = \ihat \cdot \khat = \jhat \cdot \khat = 0 $$

Therefore most of the terms cancel and we are left with what we stated as Definition #2 above:

$$ \vec{u} \cdot \vec{v} = u_x v_x + u_y v_y + u_z v_z $$

This component-based description is interesting in the sense that it's kind of like regular 1 dimensional multiplication except you multiply only the parts of the vector that are in the same direction.

Now lets see what happens when we dot a vector, $$ \vec{u} = (u_x, u_y, u_z) $$ with the standard unit vectors in $$\mathbb{R}^3$$.

$$
\begin{aligned}
\vec{u} \cdot \ihat
= \langle u_x, u_y, u_z \rangle \cdot \langle 1, 0, 0 \rangle
= \langle u_x, 0, 0 \rangle \\
\vec{u} \cdot \jhat
= \langle u_x, u_y, u_z \rangle \cdot \langle 0, 1, 0 \rangle
= \langle 0, u_y, 0 \rangle \\
\vec{u} \cdot \khat
= \langle u_x, u_y, u_z \rangle \cdot \langle 0, 0, 1 \rangle
= \langle 0, 0, u_z \rangle
\end{aligned}
$$

Again we find that the dot product is a useful tool for finding the projection of a vector in the direction of a unit vector.

# The Dot/Inner and Outer Product

We can also write the dot product, aka inner product, as the following matrix multiplication:

$$
\begin{aligned}
\text{inner product} = \vec{u} \cdot \vec{v} = \vec{u}^\intercal \vec{v}
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
\text{outer product} = \vec{u} \otimes \vec{v}
= \vec{u} \vec{v}^\intercal
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

Lagrange's Identity is analogous to pythagorous for vector multiplication.
It shows us that the dot and cross products are two parts of the whole.

$$
\begin{aligned}
\lvert \vec{a} \times \vec{b} \rvert
&= \lvert \vec{a} \rvert \lvert\vec{b} \rvert \sin{\theta} \\
{\lvert \vec{a} \times \vec{b} \rvert}^2
&= {\lvert \vec{a} \rvert}^2 {\lvert\vec{b} \rvert}^2 \sin{\theta}^2 \\
{\lvert \vec{a} \times \vec{b} \rvert}^2
&= {\lvert \vec{a} \rvert}^2 {\lvert\vec{b} \rvert}^2 (1 - \cos{\theta}^2) \\
{\lvert \vec{a} \times \vec{b} \rvert}^2
&= {\lvert \vec{a} \rvert}^2 {\lvert\vec{b} \rvert}^2 - {\lvert \vec{a} \rvert}^2 {\lvert\vec{b} \rvert}^2\cos{\theta}^2 \\
{\lvert \vec{a} \times \vec{b} \rvert}^2
&= {\lvert \vec{a} \rvert}^2 {\lvert\vec{b} \rvert}^2 - ({\lvert \vec{a} \rvert} {\lvert\vec{b} \rvert} \cos{\theta} )^2 \\
{\lvert \vec{a} \times \vec{b} \rvert}^2
&= {\lvert \vec{a} \rvert}^2 {\lvert\vec{b} \rvert}^2 - \lvert \vec{a} \cdot \vec{b} \rvert^2 \\
\end{aligned}
$$

$$ \boxed{
{\lvert \vec{a} \rvert}^2 {\lvert\vec{b} \rvert}^2
= {\lvert \vec{a} \times \vec{b} \rvert}^2 + \lvert \vec{a} \cdot \vec{b} \rvert^2
} $$

TODO

# The Wedge Product

You might think of the wedge product as analagous to the cross product but in a way that isn't limited to 3 dimensions like the cross product is. This is sometimes referred to as the exterior product.

$$ \vec{a} \times \vec{b} \text{ ... analagous to ... } \vec{a} \wedge \vec{b} $$

TODO

# Geometric Algebra

The big idea of geometric algebra (aka Clifford Algebra) is to explicitly define vector multiplication in the following way:

$$ \vec{a} \vec{b} = \vec{a} \cdot \vec{b} + \vec{a} \wedge \vec{b} $$

TODO