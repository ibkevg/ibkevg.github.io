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

# Scalar Multiplication

Multiplying a vector by a scalar produces another vector.

$$
\vec{u}
= a \vec{v}
= a \begin{bmatrix} v_x \\ v_y \end{bmatrix} = \begin{bmatrix} a v_x \\ a v_y \end{bmatrix}
$$

Much of the intuition from multipling two scalars applies when multiplying a vector by a scalar: If we multiply a vector by 1, it stays exactly the same. If we multiply a vector by 2, it becomes twice as long. If we multiply by 1/2, it shrinks in half. The scalar's sign affects the vector direction: if we multiply a vector by -1, it stays the same length but reverses direction. 

<script>  
    var ggbApp2 = new GGBApplet({"appName": "geometry", "material_id":"jh2hvwhs", "width": 400, "height": 175, "allowStyleBar": false, "showToolBar": false, "showAlgebraInput": false, "showMenuBar": false }, true);
    window.addEventListener("load", function() { 
        ggbApp2.inject('ggb-ScalarMultiplication');
    });
</script>
<div id="ggb-ScalarMultiplication"></div>

## The Null or Zero Vector

So what happens if we multiply a vector by the scalar 0? We get the null vector aka the zero vector, $$\vec{0}$$.

$$
\begin{align}
\vec{u}
&= 0 \vec{v} = \vec{0} \\
&= 0 \begin{bmatrix} v_x \\ v_y \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}
\end{align}
$$

That doesn't seem particularly startling because after all anything times 0 is 0, right? Except... we're dealing with vectors now and while it makes sense that $$ \vec{v} $$'s length becomes zero, what happens to it's direction?

There are several ways to look at this. One is that it has no direction at all. The direction a vector points in is the triangle formed by the vector line, drawn tip to tail, and a reference, say the X axis. If the length from tip to tail is 0 we have no line to measure an angle from! It's a point in space rather than a line and a point can't have an angle.

Another, opposite, way to look at this is that the null vector is pointing in all directions at once because all vectors of all directions, shrink in the limit down to the null vector:

$$ \lim_{r \to 0} r \angle{\theta }= \vec{0} $$

Given this limit, you could also think of the null vector as pointing in every direction. It might seem contradictory to say that the null vector is both "every direction" and "no particular direction" but really it's just wordsmithing and these are just different ways of phrasing the same thing.

Finally we could think of this physically. If we have a velocity vector and multiply it by 0 to bring our speed to 0, then what direction are we moving? A velocity vector, by definition, is a speed and direction of movement. So if the speed is 0, then there can be no direction of movement.

So for $$\vec{0}$$, the magnitude is zero, but the direction is unspecified.

## Unit Vectors

Scalar multiplication is also handy for creating and using unit vectors. You can think of a unit vector as representing only a direction but it's defined in such a way that it's easy to turn it into a vector of any length you might need. This was done by giving it the length of 1, so you can multiply it by any scalar magnitude to create vectors of any length you need.

You might think that for a vector to represent a direction alone it should have no notion of length at all, i.e. if the vector is $$ (r, \angle{\theta}) $$, it's corresponding unit vector might be just the $$ \angle{\theta} $$ part (i.e. just the angle.) But as we just learned, a vector with no length is the zero vector, $$ \vec{0} $$ and the zero vector has no particular direction. All that to say, for a vector to have a direction it must also have a length.

We write unit vectors with a hat. For example, $$ \hat{a} $$ is a unit vector in the direction of $$ \vec{a} $$.

To make a unit vector, say $$ \hat{u} $$, we take a vector and divide out it's magnitude, in effect normalizing it to 1.

$$ \hat{u} = \frac{\vec{u}}{\lvert\vec{u}\rvert} $$

Where a vector's magnitude is:

$$ \lvert\vec{u}\rvert = \sqrt{u_x^2 + u_y^2 + u_z^2} $$

To recreate the original vector we combine the two using the following scalar multiplication:

$$ \vec{u} = \lvert\vec{u}\rvert \hat{u} $$

Unit vectors have many uses, for example, $$ \mathbb{R}3 $$ has standard unit vectors that form the foundation of it's (x, y, z) coordinate system:

$$
\begin{align}
\ihat &= (1,0,0) \\
\jhat &= (0,1,0) \\
\khat &= (0,0,1) \\
\end{align}
$$

Any vector in $$ \mathbb{R}3 $$ can be written as a linear combination of these standard unit vectors:

$$ \vec{u} = u_x \ihat + u_y \jhat + u_z \khat $$

# Vector/Vector Products

Vector products can be tricky to understand at first because it's not obvious how we should extend our experience multiplying two numbers together to account for the directionality that vectors have. So before we introduce the equations that define dot and cross products, lets check if the dot and cross products have, at their core, the ordinary multiplication of vector lengths as you might expect.

To do this, let's express our vectors as the product of a magnitude and a unit vector and then track how each part influences the dot and cross products $$ \vec{a} \cdot \vec{b} $$ and $$ \vec{a} \times \vec{b} $$.

$$ \vec{a} = \lvert\vec{a}\rvert \hat{a} $$

$$ \vec{b} = \lvert\vec{b}\rvert \hat{b} $$

>Note: we also need to know how the dot and cross products behave under scalar multiplication. For now, please accept that the following properties are true:\\
\\
$$ (c \vec{a}) \cdot \vec{b} = \vec{a} \cdot (c \vec{b}) = c (\vec{a} \cdot \vec{b}) $$ \\
$$ (c \vec{a}) \times \vec{b} = \vec{a} \times (c \vec{b}) = c (\vec{a} \times \vec{b}) $$

Working this out, we can see that indeed for both vector products we begin by multiplying the vector lengths together:

$$ \begin{align}
\vec{a} \cdot \vec{b} = (\lvert\vec{a} \rvert \hat{a}) \cdot (\lvert\vec{b} \rvert \hat{b})
&= \lvert \vec{a} \rvert \lvert \vec{b} \rvert (\hat{a} \cdot \hat{b})\\
\vec{a} \times \vec{b} = (\lvert\vec{a} \rvert \hat{a}) \times (\lvert\vec{b} \rvert \hat{b})
&= \lvert \vec{a} \rvert \lvert \vec{b} \rvert (\hat{a} \times \hat{b})
\end{align} $$

Where the magic happens is how the dot and cross products vary in how they account for the vector directions. As we'll see below, the dot product of the unit vectors scales the result according to how parallel the vectors are while the cross product of two vectors is another vector that is perpendicular to both.


# Dot Product

A dot product takes two vectors and produces a number that represents the degree to which the two vectors point in the same direction. The closer they are to pointing in the same direction, the larger the result will be and if they are not parallel at all, then the result will be 0. So what does all this have to do with multiplication? When the dot product is largest because the vectors are both pointing in the same direction, the result is the two lengths multiplied together. So the dot product combines both multiplying the vector lengths with measuring how parallel the vectors are.

Since it produces a number, it is sometimes referred to as the Scalar Prodcut.

## Definition

Let's start with two ways to define the dot product: one from the perspective of geometry, where a vector has a length and a direction and the other from the perspective of algebra and coordinates:

__Definition #1:__ $$ \vec{u} \cdot \vec{v} = \lvert u \rvert \lvert v \rvert \cos {\theta} $$ \\
__Definition #2:__ $$ \vec{u} \cdot \vec{v} = u_x v_x + u_y v_y + u_z v_z $$

A way to think of this is the dot product multiplies the magnitudes of two vectors _but only the parts that lie in the same direction_. The geometric viewpoint does this all at once via $$ \cos{\theta} $$ whereas the algebraic viewpoint accomplishes this by multiplying like components together.

We will explore what this means in detail but for now just play around with the example by dragging the vectors around and observing that effect of making the vectors longer, shorter, more parallel and more perpendicular have on the dot product.

Notice also that if the vectors are 1 dimensional, then the dot product simplifies to the usual multiplying two numbers together.

<script>  
    var ggbApp = new GGBApplet({"appName": "geometry", "material_id":"e5hhjxct", "width": 300, "height": 250, "allowStyleBar": false, "showToolBar": false, "showAlgebraInput": false, "showMenuBar": false }, true);
    window.addEventListener("load", function() { 
        ggbApp.inject('ggb-DotProduct');
    });
</script>
<div id="ggb-DotProduct"></div> 

Now to develop our intuition, let's first try this out with some simple vectors, $$ \ihat $$ and $$ \jhat $$ the x and y axis unit vectors.

$$
\begin{align}
\ihat \cdot \ihat &= (1)(1) \cos 0 = 1  \\
\ihat \cdot \jhat &= (1)(1) \cos 90^\circ = 0 \\
\jhat \cdot \jhat &= (1)(1) \cos 0 = 1
\end{align}
$$

So as expected, we find:

$$
\begin{align}
\vec{u} \cdot \vec{v} &= 0 \text{, when } \vec{u} \perp \vec{v} \\
\vec{u} \cdot \vec{v} &= \lvert\vec{u}\rvert \lvert\vec{v}\rvert \text{, when } \vec{u} \parallel \vec{v}
\end{align}
$$

So the dot product can be a handy way to find out if two vectors are perpendicular or not. If dotting them produces 0 then they are perpendicular. Another way this can be useful is if you want to find a line that is perpendicular to the one you have.

Next lets see what happens when we dot a regular vector, $$ \vec{u} = ( r, \angle \theta) $$, with these same unit vectors.

$$
\begin{align}
\vec{u} \cdot \ihat &= r (1) \cos{\theta} &= r \cos \theta \\
\vec{u} \cdot \jhat &= r (1) \cos{90^\circ - \theta} &= r \sin \theta
\end{align}
$$

Here we find that the dot product has given us the projection of the vector onto the x and y axis respectively, something done frequently in engineering and physics.

Now we are finally in a position to see how the dot product works. If instead of a unit vector we used a second regular vector, we would still have the $$ r \cos \theta $$ part but instead of (1) for the unit vector we will have the magnitude of the second vector. It's saying take all of the second vector and multiply it by the amount of the first vector that lies in the same direction. Conversely you could think of the projection being from the second onto the first, it doesn't matter.

Now lets look at how the coordinate oriented definition #2 can be derived from definition #1. Here we write $$ \vec{u} $$ and $$ \vec{v} $$ as a linear combination of the standard $$ \mathbb{R}3 $$ unit vectors:

$$
\begin{align}
\vec{u} &= u_x \ihat + u_y \jhat + u_z \khat \\
\vec{v} &=  v_x \ihat + v_y \jhat + v_z \khat
\end{align}
$$

Now we can write out the dot product as:

$$
\begin{align}
\vec{u} \cdot \vec{v} = \;
&\begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix} \cdot
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix} \\
= \; &u_x v_x \ihat \cdot \ihat + u_x v_y \ihat \cdot \jhat + u_x v_z \ihat \cdot \khat +\\
&u_y v_x \jhat \cdot \ihat + u_y v_y \jhat \cdot \jhat + u_y v_z \jhat \cdot \khat +\\
&u_z v_x \khat \cdot \ihat + u_z v_y \khat \cdot \jhat + u_z v_z \khat \cdot \khat
\end{align}
$$

Remember that above we found:

$$
\ihat \cdot \ihat = \jhat \cdot \jhat = \khat \cdot \khat = 1 \\
\ihat \cdot \jhat = \ihat \cdot \khat = \jhat \cdot \khat = 0
$$

Therefore most of the terms cancel and we are left with what we stated as Definition #2 above:

$$ \vec{u} \cdot \vec{v} = u_x v_x + u_y v_y + u_z v_z $$

This component-based description is interesting in the sense that it's kind of like regular 1 dimensional multiplication except you multiply only the parts of the vector that are in the same direction.

Notice that we can also write this as the following matrix multiplication:

$$
\begin{align}
\vec{u} \cdot \vec{v} = \vec{u}^\intercal \vec{v}
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
= u_x v_x + u_y v_y + u_z v_z
\end{align}
$$

Now lets see what happens when we dot a vector, $$ \vec{u} = (u_x, u_y, u_z) $$ with the standard unit vectors in $$\mathbb{R}3$$.

$$
\begin{align}
\vec{u} \cdot \ihat = \begin{pmatrix} u_x & u_y & u_z \end{pmatrix} \cdot \begin{pmatrix} 1 & 0 & 0 \end{pmatrix} = \begin{pmatrix} u_x & 0 & 0 \end{pmatrix} \\
\vec{u} \cdot \jhat = \begin{pmatrix} u_x & u_y & u_z \end{pmatrix} \cdot \begin{pmatrix} 0 & 1 & 0 \end{pmatrix} = \begin{pmatrix} 0 & u_y & 0 \end{pmatrix} \\
\vec{u} \cdot \khat = \begin{pmatrix} u_x & u_y & u_z \end{pmatrix} \cdot \begin{pmatrix} 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 0 & 0 & u_z \end{pmatrix}
\end{align}
$$

Again we find that the dot product is a useful tool for finding the projection of a vector in the direction of a unit vector. We can generalize this to finding the projection in the direction of any vector using:

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
