---
title: Vector Basics
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

# Vectors

A vector is just a list of objects that are related in some way. The list describes properties of something that we need to keep separate but are still related and need to mathematically be treated in a way that makes sense for them as a group. For example:
* $ \vec p = (x,y,z) $ : a vector position, $ \vec p $, could contain the (x, y, z) components of the position
* $ \vec F = (F_x, F_y, F_z) $ : a vector force
* $ \vec f = (apples, oranges) $ : a fruit vector might contain both (apples, oranges). We can't mix apples and oranges together so we have to keep count of them separately. That said, some things are convenient to do to both at the same time, for example, we could to triple the stock of all fruit by multiplying the fruit vector by 3, this would cause both apple and orange values to individually increase by a factor of 3.

# Vector Operations
## Scaling Vectors

We scale a vector by multiplying by a scalar value.

$$
x \vec v = x
\begin{bmatrix}
a \\
b 
\end{bmatrix}
= \begin{bmatrix}
ax \\
bx
\end{bmatrix}
$$

So, for example:

$$
3
\begin{bmatrix}
1 \\
2 
\end{bmatrix}
= \begin{bmatrix}
3 \\
6
\end{bmatrix}
$$

## Adding Vectors

$$
\vec u + \vec v
= \begin{bmatrix}
a \\
b 
\end{bmatrix} +
\begin{bmatrix}
c \\
d
\end{bmatrix}
= \begin{bmatrix}
a+c \\
b+d
\end{bmatrix}
$$

So, for example:

$$
\begin{bmatrix}
1 \\
2 
\end{bmatrix}
+
\begin{bmatrix}
3 \\
4
\end{bmatrix}
= \begin{bmatrix}
4 \\
6
\end{bmatrix}
$$

## Scalar Multiplication

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

# The Null or Zero Vector

If we multiply a vector by zero, we get a null vector aka a zero vector, $\vc{0}$.

$$ 0 \vc{v} = \vc{0} $$

That doesn't seem particularly startling because after all anything times 0 is 0, right? So lets explore what this means in terms of rectangular coordinates and then geometrically.

$$
0 \vc{v} 
= 0 \begin{bmatrix} v_x \\ v_y \end{bmatrix}
= \begin{bmatrix} 0v_x \\ 0v_y \end{bmatrix}
= \begin{bmatrix} 0 \\ 0 \end{bmatrix}
$$

Here we find that a Null vector has no direction at all because there's no way to measure the angle between two lines of 0 length. It's like asking what is the angle of a plate of spaghetti? It's a question that doesn't have a meaningful answer.

Now how should we think of this in geometry, length and angle, terms? It makes sense that $ \vc{v} $'s length becomes zero, but what happens to it's direction?

$$ 0 \vc{v} = 0 \langle r, \angle{\theta } \rangle = \langle 0, \angle{???} \rangle $$

We could think of a null vector as pointing in any direction because all vectors, of all directions, shrink in the limit down to a null vector:

$$ \lim_{r \to 0} \langle r, \angle{\theta } \rangle = \vc{0} $$

But then what angle should the zero vector have here:

$$ \vc{a} + (-\vc{a}) = \vc{0} $$

So the reality is that a vector's direction is only meaningful when accompanied by a non-zero length. It might seem contradictory to say that a null vector is both "any direction" and "no particular direction" but these are really just different ways to express in english that it is mathematically undefined.

So for $\vc{0}$, the length is zero, and the direction is undefined.

# Vector Length or Norm

A vector's length is:

$$ \lvert\vc{u}\rvert = \sqrt{u_x^2 + u_y^2 + u_z^2} $$


# Unit Vectors

Scalar multiplication is also useful for creating and using unit vectors.

A unit vector is a handy way to represent a direction without a specific magnitude. Notationally, we write it with a hat, for example, $ \hat{\vc{a}} $ is a unit vector in the direction of $ \vc{a} $.

You might think that for a vector to represent a direction alone it should have no notion of length at all, i.e. if the vector is $ \langle r, \angle{\theta} \rangle $, it's corresponding unit vector might be just the angle. But as we just learned, a vector with no length is a zero vector, $ \vc{0}, $ and a zero vector's direction is undefined. So, for a vector to have a direction it must also have a length. Having "unit" in the name gives us a hint as to what it's length is because unit means 1 and that is the length of a unit vector.

The reason unit vectors are so handy is because anything times 1 is itself, thus unit vectors can be multiplied by any scalar to create vectors of any length you need. As an example, we can make a $ \vc{b} $ in the direction of $ \hat{\vc{a}} $ using $ \vc{b} = 5 \hat{\vc{a}} $. So, $ \vc{b} $ has length, $ \lvert\vc{b}\rvert = 5 $.

To make $ \hat{\vc{a}} $, we take vector $ \vc{a} $ and divide out it's length, $ \lvert\vc{a}\rvert $, in effect normalizing it's components to 1.

$$ \hat{\vc{u}} = \frac{\vc{u}}{\lvert\vc{u}\rvert} $$

where a vector's length is:

$$ \lvert\vc{u}\rvert = \sqrt{u_x^2 + u_y^2 + u_z^2} $$

To recreate the original vector we combine the two using the following scalar multiplication:

$$ \vc{u} = \lvert\vc{u}\rvert \hat{u} $$

Unit vectors have many uses, for example, $ \mathbb{R}^3 $ has standard unit vectors that form the foundation of the (x, y, z) coordinate system:

$$
\begin{aligned}
\ihat &= \langle 1,0,0 \rangle \\
\jhat &= \langle 0,1,0 \rangle \\
\khat &= \langle 0,0,1 \rangle \\
\end{aligned}
$$

Any vector in $ \mathbb{R}^3 $ can be written as a linear combination of these standard unit vectors:

$$ \vc{u} = u_x \ihat + u_y \jhat + u_z \khat $$

# Vector to Vector Products

The dot product of A and B is written $ \vc{a} \cdot \vc{b} $ and provides a measure of how parallel the vectors are. It is the length of the projection of A onto B multiplied by the length of B (or the other way around--it's commutative).

The cross product of A and B is written $ \vc{a} \times \vc{b} $ and provides a measure of how perpendicular the vectors are. The magnitude of the cross product is the area of the parallelogram with two sides A and B. The orientation of the cross product is orthogonal to the plane containing this parallelogram.

Vector to vector products can be tricky to understand at first because it's not obvious how we should extend our experience multiplying two numbers together to account for the directionality that vectors have. So before we introduce the equations that define dot and cross products, lets check if the dot and cross products have, at their core, the ordinary multiplication of vector lengths as you might expect.

To do this, let's express our vectors as the product of a length and a unit vector and then track how each part influences $ \vc{a} \cdot \vc{b} $ and $ \vc{a} \times \vc{b} $.

$$ \vc{a} = \lvert\vc{a}\rvert \hat{a} $$

$$ \vc{b} = \lvert\vc{b}\rvert \hat{b} $$

>Note: we also need to know how the dot and cross products behave under scalar multiplication. For now, please accept that the following properties are true:  
> $ (c \vc{a}) \cdot \vc{b} = \vc{a} \cdot (c \vc{b}) = c (\vc{a} \cdot \vc{b}) $
> $ (c \vc{a}) \times \vc{b} = \vc{a} \times (c \vc{b}) = c (\vc{a} \times \vc{b}) $

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
