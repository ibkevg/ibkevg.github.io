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

Testing $ \vc{a} $ testing 1 2 3.

There are lots of ways to multiply vectors

| *Notation* | *Description* | *Produces ...* |  
| $ a \vc{u} $ | scalar multiplication| vector |  
| $$ \vc{u} \cdot \vc{v} $$ | dot product (aka scalar product) | scalar |  
| $$ \vc{u} \times \vc{v} $$ | cross product | vector |  
| $$ \inner{\vc u}{\vc v} $$ | inner product (~= dot product) | scalar |  
| $$ \vc{u} \otimes \vc{v} $$ | outer product (aka tensor product) | tensor, multilinear matrix |  
| $$ \vc{u} \wedge \vc{v} $$ | exterior product (aka wedge product) | bivector |  
| $$ \vc{u}\vc{v} = \vc{u} \cdot \vc{v} + \vc{u} \wedge \vc{v} $$ | geometric product | multivector |  

My goal here is to:

1. show how these vector operations work
1. help build intuition about what they really mean
1. provide examples of how to use them
1. show why the vector products took the form that they do and not some other form

# What was Hamilton looking for?

One good way (especially in the present context) of describing Hamilton’s search for quaternions is to state that his search was for numbers with the following six characteristics, all of which are found in ordinary complex numbers: (1) associativity for multiplication and division, (2) commutativity for addition and multiplication, (3) the distributive property, (4) the property that division is unambiguous, (5) the property that the numbers obey the law of the moduli,4 (6) the property of being useful for the analysis of three-dimensional space. Quaternions possess all of six characteristics, with the exception that they are not commutative for multiplication. One can get a sense of why quaternionists objected to modern vector analysis when it is noted that modern vector analysis involves two forms of multiplication, the scalar (dot) and vector (cross) products. For the scalar product, associativity is irrelevant, and both the law of the moduli and unambiguity of division must be abandoned. For the vector product, the associative and commutative properties must be abandoned, division is not unambiguous, and the law of the moduli fails as well.

# What does a vector product even mean?

Our intuition and expectations for what it means to calculate a product is initially formed from multiplying two ordinary numbers together. When we start considering the product of two vectors it's not obvious how we should extend our intuition to account for the directionality that vectors have.

Imagine this is the formative period when vectors were being invented/discovered and we have figured out how to add, subtract and multiply vectors by a scalar and are now embarking on vector products. We quickly run into the problem that we can imagine all kinds of different ways to slice, dice and combine vector components, but by what criteria would we know when we've found one that is "correct"? Or, if you think of math as invented, then what would your feature list be?

For example, when we multiply two numbers, say 5 x 4, we sometimes think of it as shortcut for 5 + 5 + 5 + 5. So should we think of vector multiplication similarly, as repeated sums? This way of thinking gets trickier to hold on to when we consider multiplying real numbers, say 5.2 x 4.75. We might imagine how fractional parts can play into a repeated sum if we stand on our heads and squint a bit, but it's getting tenuous. As you might be starting to suspect, in mathematics a product is not defined as the sum of a repeated addition.

Maybe it is defined somewhere what a product must do? In advanced mathematics there are all kinds of "objects" that can be manipulated using algebra in addition to numbers such as complex numbers and vectors and matricies and sets and groups and rings, etc. Surely there is some universal definition of product that applies to all these things. ie. if someone were to invent a new abstract math object along with the operations you can perform on them, then this universal definition would tell us which of the operations should be considered products.

You may be surprised to learn that there is no universal definition and whether an operation is thought of as multiplicative or not (and labelled a product) is determined by history and convention. For example, convention might be drawn from similarity with multiplication of regular numbers. The same is true for other operations such as addition.

So it seems we have a lot of latitude. Lets base our expections for vector multiplication on how regular numbers behave:

1. should have useful applications
2. should have geometric meaning
3. should work the same as regular number multiplication
4. should support division that works the same as regular number division
5. regular number multiplication should be just a special case
6. should be closed under multiplication, just like reals and complex numbers

**Has useful applications**  

I think this says it all:
>"It looks fucking great actually! Yeah, really nice. It's beautiful... but it's useless. And as William Morris once said: "Nothing useless can be truly beautiful." - Tony Wilson, 24 Hour Party People

**Has Geometric Meaning**

Geometrically, the multiplication of reals relates to area. Also it relates to scaling values larger and smaller. Also, the multiplication of complex numbers relates to rotation in the plane formed by a real and imaginary axis. So it seems reasonable that whatever we come up with for vector multiplication of vectors could have elements of both of those things.

**Should Work the Same as Regular Number Multiplication**

Ideally we could work algebraically with vector multiplication the same as we do with regular numbers. No special rules to remember. When we say that, we mean we want them to support the same set of properties.

_Properties of Multiplication_

Commutative Property: $$ \vc{a}\vc{b} = \vc{b}\vc{a} $$  
Associative Property: $$ \vc{a}(\vc{b}\vc{c}) = (\vc{a}\vc{b})\vc{c} $$  
Distributive Property: $$ \vc{a} (\vc{b} + \vc{c} ) = \vc{a}\vc{b} + \vc{a}\vc{c} $$  

Many of these seem like they're stating the obvious, however its useful to be explicit when listing requirements.

**Supports Division**

When we say we want division to exist and work for vectors the same as it does for regular numbers, we again mean we want them to support the same set of properties.

_Properties of Division_

Multiplicative Identity: $$ 1\vc{a} = \vc{a} $$ (Note that this is required for division to exist.)
Multiplicative Inverse (or reciprocal): $$ \vc{a} \vc{a}^{-1} = \vc{a}^{-1} \vc{a} = 1 $$

Division is not commutative: $$ \vc{a} \div \vc{b} \neq \vc{b} \div \vc{a} $$

$$ \frac{\vc{a}}{\vc{b}} \ne \frac{\vc{b}}{\vc{a}} $$

Division is also not associative: $$ \vc{a} \div (\vc{b} \div \vc{c}) \neq (\vc{a} \div \vc{b}) \div \vc{c} $$

$$ \frac{\vc{a}\vc{c}}{\vc{b}} \ne \frac{\vc{a}}{\vc{b}\vc{c}} $$  

Division is right distributive: $$ (\vc{a}+\vc{b}) ÷ \vc{c} = (\vc{a} ÷ \vc{c}) + (\vc{b} ÷ \vc{c}) $$

$$ \frac{\vc{a} + \vc{b}}{\vc{c}} = \frac{\vc{a}}{\vc{c}} + \frac{\vc{b}}{\vc{c}} $$

Division is not left distributive: $$ \vc{c} \div (\vc{a}+\vc{b}) = (\vc{c} ÷ \vc{a}) + (\vc{c} ÷ \vc{b}) $$

$$ \frac{\vc{c}}{\vc{a} + \vc{b}} \ne \frac{\vc{c}}{\vc{a}} + \frac{\vc{c}}{\vc{b}} $$  

**Regular number multiplication is just a special case**

It would be beautiful if ordinary regular number multiplcation fell out of our new vector/vector product as a special case.

**Closed under multiplication**

Ideally, we hope that multiplying two vectors would result in another vector, just the same as happens when multiplying reals or complex numbers.

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

So the reality is that a vector's direction is only meaningful when accompanied by a non-zero length. It might seem contradictory to say that a null vector is both "any direction" and "no particular direction" but these are really just different ways to express in english that it is mathematically undefined.

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
\ihat &= \langle 1,0,0 \rangle \\
\jhat &= \langle 0,1,0 \rangle \\
\khat &= \langle 0,0,1 \rangle \\
\end{aligned}
$$

Any vector in $$ \mathbb{R}^3 $$ can be written as a linear combination of these standard unit vectors:

$$ \vc{u} = u_x \ihat + u_y \jhat + u_z \khat $$

# Vector to Vector Products

The dot product of A and B is the length of the projection of A onto B multiplied by the length of B (or the other way around--it's commutative).

The magnitude of the cross product is the area of the parallelogram with two sides A and B. The orientation of the cross product is orthogonal to the plane containing this parallelogram.




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

Since it produces a number, it is sometimes referred to as the Scalar Product.

## Definition

We will define the dot product in two different ways. Once from the perspective of geometry, where a vector has a length and a direction and the other from the perspective of algebra where a vector is comprised of coordinates. Let's start with the geometric viewpoint:

__Geometric Definition:__ $$ \vc{u} \cdot \vc{v} = \lvert u \rvert \lvert v \rvert \cos {\theta} $$  

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

If we now substitute

$$ \hat{a} = \frac{\vc{a}}{\lvert a \rvert} \;\;\; \hat{b} = \frac{\vc{b}}{\lvert b \rvert} $$

we get the original definition:

$$ \vc{a} \cdot \vc{b} = \lvert a \rvert \lvert b \rvert \cos {\theta} $$  

### Geometric Interpretation #2: Parallel and Perpendicular Vectors

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

### Geometric Interpretation #3: Projections

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

### Geometric Interpretation #4: Projection + Multiplication

Now we are in a position to put this all together. If instead of a unit vector we used a second regular vector, we would still have the $$ r \cos \theta $$ part but instead of (1) for the unit vector we will have the length of the second vector. It's saying take all of the second vector and multiply it by the amount of the first vector that lies in the same direction. Conversely you could think of the projection being from the second onto the first. It's symmetric so it doesn't matter.

### Dot Product using Coordinates

__Algebraic Definition:__ $$ \vc{u} \cdot \vc{v} = u_x v_x + u_y v_y + u_z v_z $$

Remember that the dot product multiplies two vectors _but only the parts that lie in the same direction_, when dealing with coordinates, this is accomplished by multiplying like components together.

Now lets look at how the algebraic definition can be derived from the geometric definition. Here we write $$ \vc{u} $$ and $$ \vc{v} $$ as a linear combination of the standard $$ \mathbb{R}^3 $$ unit vectors:

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

This component-based description is interesting because it really makes clear that only like components of the two vectors are being multiplied.

Now lets see what happens when we dot a vector, $$ \vc{u} = \langle u_x, u_y, u_z \rangle $$ with the standard unit vectors in $$\mathbb{R}^3$$.

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

Examples? Work (energy) is a dot product of force and displacement. The angle between two vectors is found by knowing that the cosine of the angle between them is their dot product divided by their self dot product.

Example: The work expression $$ W = \vec{F} \cdot \vec{r} $$, where only the force component parallel to the direction (or likewise, the position component parallel to the force) is wanted.
The (magnetude of the) cross product gives you the multiplication of the perpendicular components.

You’re often interested in knowing to what extent a vector quantity contributes in a given direction (the vector quantity’s component in that direction). This is what the dot (scalar) product, as used in physics, tells you.

## Division

In order to support division we need to be able to be able to take the result of a dot product and recover one of the original vectors by dividing out the other. For this we need the properties below.

We need a multiplicative identity:

$$ 1 \cdot \vc{u} = \vc{u} $$

We need a multiplicative inverse:

$$ \vc{v} \cdot \vc{v}^{-1} = 1 $$?

If we can make those work we can define division as dotting with an inverse.

$$ \frac{\vc{a}}{\vc{b}} = \vc{a} \cdot \vc{b}^{-1} = \vc{c} $$

A scalar value of 1 works just fine for an identity but we run into a problem when we try to define the inverse of a vector. The dot product loses all directionality information and so recovering an input vector, including it's direction is impossible.

## Cross Product versus our Criteria for a "Good Product"

Let's review the dot product against our expectations:

1. Useful applications  
**Yes** We showed above that the dot product can be used to determine the angle between vectors, is useful to test perpendicularity and parallelity, find projections onto basis or other vectors, etc.  
Also an example from physics: $$ W = \vc{F} \cdot \vc{d} $$  
1. Geometric meaning  
**Yes** The dot product can be viewed as a projection-based multiply.
1. Works the same as regular number multiplication  
**Yes**
The dot product obeys the commutative, associative and distributive properties.
1. Support division that works the same as regular number division  
**No** The dot product loses information in producing it's scalar result. You can't start with a scalar dot product result and recover one of the initial vectors.
1. Regular number multiplication should be just a special case  
**Yes** If a vector has a single dimension, then the dot project becomes identical to 
1. Should be closed under multiplication, just like reals and complex numbers  
**No** Dot product of two vectors produces a scalar. Why doesn't it produce a vector? Because it is symmetrical, you could think of it as a projection of either vector onto the other. So it would have to choose the dirction of one of the vectors.

So it's a pretty good multiply but not perfect.

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

http://en.wikipedia.org/wiki/Cross_product#History

## Cross Product versus our Criteria for a "Good Product"

Let's review the dot product against our expectations:

1. Useful applications  
**TBD**
1. Geometric meaning  
**TBD**
1. Works the same as regular number multiplication  
**TBD**
1. Support division that works the same as regular number division  
**TBD**
1. Regular number multiplication should be just a special case  
**TBD**
1. Should be closed under multiplication, just like reals and complex numbers  
**TBD**

So it's a pretty good multiply but not perfect.


## Cross Product vs Determinant

TODO

# Combining Dot and Cross Products

While dot and cross products on their own don't satisfy our requirements for multiplying vectors, we have some hints that suggest the two may be combined. Perhaps this combination does?

Earlier we learned that $$ \vc{u} \cdot \vc{v} \propto \cos{\theta} $$ and $$ \vc{u} \times \vc{v} \propto \sin{\theta} $$. This suggests we may find a pythagorean relation, $$ \sin^2 + \cos^2 = 1 $$, between them.

Also, suggesting a possible relation are the multiplication tables for both kinds of products.

Dot product multiplication table: $$
\begin{matrix}
\cdot & e_1 & e_2 & e_3 \\
e_1 & 1 & 0 & 0 \\
e_2 & 0 & 1 & 0 \\
e_3 & 0 & 0 & 1
\end{matrix} 
$$

Cross product multiplication table: $$
\begin{matrix}
\times & e_1 & e_2 & e_3 \\
e_1 & 0 & e_3 & -e_2 \\
e_2 & -e_3 & 0 & e_1 \\
e_3 & e_2 & -e_1 & 0
\end{matrix} 
$$

## Lagrange's Identity

Lagrange's Identity shows us that the dot and cross products are two parts of a greater whole. It is analogous to Pythagoras Theorem but for vector multiplication.

$$
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
= {\lvert \vc{a} \times \vc{b} \rvert}^2 + \lvert \vc{a} \cdot \vc{b} \rvert^2
$$

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
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
&= {\lvert \vc{a} \times \vc{b} \rvert}^2 + \lvert \vc{a} \cdot \vc{b} \rvert^2
\end{aligned}
$$

Or starting with the dot product:

$$
\begin{aligned}
\lvert \vc{a} \cdot \vc{b} \rvert
&= \lvert \vc{a} \rvert \lvert\vc{b} \rvert \cos{\theta} \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 \cos{\theta}^2 \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 (1 - \sin{\theta}^2) \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - ({\lvert \vc{a} \rvert} {\lvert\vc{b} \rvert} \sin{\theta} )^2 \\
{\lvert \vc{a} \cdot \vc{b} \rvert}^2
&= {\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2 - \lvert \vc{a} \times \vc{b} \rvert^2 \\
{\lvert \vc{a} \rvert}^2 {\lvert\vc{b} \rvert}^2
&= {\lvert \vc{a} \times \vc{b} \rvert}^2 + \lvert \vc{a} \cdot \vc{b} \rvert^2
\end{aligned}
$$



# Multiplying Two Quarternions

Quarternions are an extension of complex numbers. Here we write $$ \vc{u} $$ and $$ \vc{v} $$ as pure vector quarternions:

$$
\begin{aligned}
\vc{u} &= u_x \ihat + u_y \jhat + u_z \khat \\
\vc{v} &=  v_x \ihat + v_y \jhat + v_z \khat
\end{aligned}
$$

Think of i, j and k analogous to x, y, and z.

$$
\begin{aligned}
\vc{u} \vc{v}
= \; &\begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix}
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix} \\
= \;
&u_x v_x \ihat \ihat + u_x v_y \ihat \jhat + u_x v_z \ihat \khat +\\
&u_y v_x \jhat \ihat + u_y v_y \jhat \jhat + u_y v_z \jhat \khat +\\
&u_z v_x \khat \ihat + u_z v_y \khat \jhat + u_z v_z \khat \khat
\end{aligned}
$$

Just like $$ \vc{i} $$ for imaginary numbers, imagine $$ \vc{j}, \vc{k} $$ are similar:

$$ \ihat \ihat = \jhat \jhat = \khat \khat =  \ihat \jhat \khat = -1 $$

We can now derive $$ \ihat \jhat $$:

$$\begin{aligned}
\ihat \jhat \khat &= -1 \\
\ihat \jhat \khat \khat &= -1 \khat \\
\ihat \jhat (-1) &= -1 \khat \\
\ihat \jhat &= \khat \\
\end{aligned}$$

A similar process produces:

$$ \ihat \jhat = \khat \;\;\; \jhat \khat = \ihat  \;\;\; \khat \ihat = \jhat $$

Next:

$$\begin{aligned}
(\jhat \khat)(\khat \ihat) &= \ihat \jhat \\
\jhat (\khat \khat) \ihat &= \khat \\
\jhat (-1) \ihat &= \khat \\
\jhat \ihat &= -\khat \\
\end{aligned}$$

A similar process produces:

$$ \khat \jhat = -\ihat \;\;\; \jhat \ihat = -\khat \;\;\; \ihat \khat = -\jhat $$

Now we can substitute to get:

$$
\begin{aligned}
\vc{u} \vc{v}
= \;
&-(u_x v_x + u_y v_y + u_z v_z) \\
&+ (u_y v_z - u_z v_y) \ihat \\
&+ (u_z v_x - u_x v_z) \jhat \\
&+ (u_x v_y - u_y v_x) \khat \\
\vc{u} \vc{v} = \; &-(\vc{u} \cdot \vc{v}) + (\vc{u} \times \vc{v})
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

Also, regardless of perpendicularity, 2 of the vectors that form the sides of the triangle must sum to the other. We arbitrarily choose $$ \vc{a} = \vc{b} + \vc{s} $$ or $$ \vc{s} = \vc{a} - \vc{b} $$ :

$$ |\vc{s}|^2 = (a_x-b_x)^2 + (a_y-b_y)^2 + (a_z-b_z)^2 $$

Now when $$ \vc{a} \perp \vc{b} $$, we can equate $$ \abs{\vc{s}}^2 = \abs{\vc{s}}^2_{perp} $$:

$$
\begin{aligned}
(a_x-b_x)^2 + (a_y-b_y)^2 + (a_z-b_z)^2
&= (a_x^2 + a_y^2 + a_z^2)  +  (b_x^2 + b_y^2 + b_z^2) \\
a_x^2 - 2a_x b_x + b_x^2 +
a_y^2 - 2a_y b_y + b_y^2 + 
a_z^2 - 2a_z b_z + b_z^2
&= a_x^2 + a_y^2 + a_z^2 + b_x^2 + b_y^2 + b_z^2 \\
-2a_x b_x - 2a_y b_y - 2a_z b_z
&= 0 \\
a_x b_x + a_y b_y + a_z b_z &= 0
\end{aligned}
$$

This is consistent with the definition of the dot product which is 0 when the vectors are perpendicular:

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

We can equate these two expressions, $$ \abs{\vc{s}}^2 = \abs{\vc{s}}^2_{parallel} $$, when $$ \vc{a} \parallel \vc{b} $$:

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

Notice that we can gather terms and re-write this as

$$ (a_x b_y - b_x a_y)^2  +  (b_x a_z - a_x b_z)^2  +  (a_y b_z - b_y a_z)^2  =  0 $$

This sum of squares equals zero only when $$ \vc{a} \parallel \vc{b} $$ and is consistent with the definition of the cross product:

$$ \vc{a} \times \vc{b}
= \begin{bmatrix}
a_y b_z - b_y a_z \\
a_y b_z - b_y a_z \\
a_x b_y - b_x a_y
\end{bmatrix}
$$

Also as we saw previously, the dot product of two vectors is 0 if the vectors are perpendicular. We can use this to confirm the following:

that $$ \vc{a} \times \vc{b} $$ is perpendicular to $$ \vc{a} $$:

$$
\begin{aligned}
\vc{a} \cdot (\vc{a} \times \vc{b})
&= \begin{bmatrix} a_x, a_y, a_z \end{bmatrix} \cdot 
\begin{bmatrix}
a_y b_z - b_y a_z \\
a_y b_z - b_y a_z \\
a_x b_y - b_x a_y
\end{bmatrix} = 0 \\
&= a_x a_y b_z - a_x b_y a_z  +  a_y b_x a_z - a_y a_x b_z  +  a_z a_x b_y - a_z b_x a_y \\
&= 0
\end{aligned}
$$

that $$ \vc{a} \times \vc{b} $$ is perpendicular to $$ \vc{b} $$:

$$
\begin{aligned}
\vc{b} \cdot (\vc{a} \times \vc{b})
&= \begin{bmatrix} b_x, b_y, b_z \end{bmatrix} \cdot 
\begin{bmatrix}
a_y b_z - b_y a_z \\
a_y b_z - b_y a_z \\
a_x b_y - b_x a_y
\end{bmatrix} = 0 \\
&= b_x a_y b_z - b_x b_y a_z  +  b_y b_x a_z - b_y a_x b_z  +  b_z a_x b_y - b_z b_x a_y \\
&= 0 
\end{aligned}
$$


# The Wedge Product

You might think of the wedge product as analagous to the cross product but in a way that isn't limited to 3 dimensions like the cross product is. This is sometimes referred to as the exterior product.

$$ \vc{a} \times \vc{b} \text{ ... analagous to ... } \vc{a} \wedge \vc{b} $$

TODO

# Geometric Algebra

The big idea of geometric algebra (aka Clifford Algebra) is to explicitly define vector multiplication in the following way:

$$ \vc{a} \vc{b} = \vc{a} \cdot \vc{b} + \vc{a} \wedge \vc{b} $$

Think of the sum as like the real and imaginary parts of a complex number.


## Division

The question "what does $$ \vc{a} / \vc{b} $$ equal?" is equivalent to asking "What do you multiply with $$ \vc{b} $$ to get $$ \vc{a} $$?"

How would you define the inverse of a vector such that $$ \vc{v}\vc{v}^{-1} = 1 $$? What would be the "identity vector" 1

In fact, the answer is sometimes you can. In particular, in two dimensions, you can make a correspondence between vectors and complex numbers, where the real and imaginary parts of the complex number give the (x,y) coordinates of the vector. Division is well-defined for the complex numbers.

The cross-product only exists in 3D.

Division is defined in some higher-dimensional spaces too (such as the quaternions), but only if you give up commutativity and/or associativity.

For ordinary numbers, I think of $$ x/y $$ as being the number that, when multiplied by $$ y $$, gives $$ x $$. So, $$ \vc{x} / \vc{y} $$ would have to be the vector that, when "multiplied" by $$ \vc{y} $$, gives $$ \vc{x} $$. If our multiplication involves the dot product, we're already in trouble, because the dot product of two vectors is a scalar, and the definition above would therefore require $$ \vc{x} / \vc{y} $$ to simultaneously be a vector and a scalar.

QUESTION: WHY DO WE KNOW THIS? IS IT A PROPERTY? Similarly, if our operation is the cross product, then we know that, for any vectors 𝑥⃗ and 𝑦⃗
 and any scalar 𝑐, we have 𝑥⃗×𝑦⃗=𝑥⃗×(𝑦⃗+𝑐𝑥⃗), so this means that there are an infinite number of vectors that satisfy the property "when crossproducted by 𝑦⃗, gives 𝑥⃗". Therefore, division over the cross product is not unique.




You can divide vectors with clifford ("geometric") algebra.

The geometric product of vectors is associative: 𝑎𝑏𝑐=(𝑎𝑏)𝑐=𝑎(𝑏𝑐)

And the geometric product of a vector with itself is a scalar.

𝑎𝑎=|𝑎|2

These are all the properties required to define a unique product of vectors. All other properties can be derived. I'll sum them up, however: for two vectors, the geometric product marries the dot and cross products.

𝑎𝑏=𝑎⋅𝑏+𝑎∧𝑏

We use wedges instead of crosses because this second term is not a vector. We call it a bivector, and it represents an oriented plane. It can be instructive to introduce a basis to see this. 𝑒1𝑒1=𝑒2𝑒2=1 and 𝑒1𝑒2=−𝑒2𝑒1 capture the geometric product's properties for these orthonormal basis vectors. The geometric product is then,

𝑎𝑏=(𝑎1𝑒1+𝑎2𝑒2)(𝑏1𝑒1+𝑏2𝑒2)=(𝑎1𝑏1+𝑎2𝑏2)+(𝑎1𝑏2−𝑎2𝑏1)𝑒1𝑒2

As I said, the geometric product of two vectors is invertible in Euclidean space. This is obvious from the associativity property: 𝑎𝑏𝑏−1=𝑎(𝑏𝑏−1)=𝑎. That 𝑏𝑏−1=1 implies that 𝑏−1=𝑏/|𝑏|2

It's informative to look at the quantity 𝑎=(𝑎𝑏)𝑏−1, using the grouping to decompose it a different way.

𝑎=(𝑎𝑏)𝑏−1=(𝑎⋅𝑏)𝑏−1+(𝑎∧𝑏)⋅𝑏−1

The first term is in the direction of 𝑏, the second is orthogonal to 𝑏. This decomposes 𝑎
a into 𝑎∥ and 𝑎⊥.

What others have said is right, you can't define just the vector cross product to be invertible. This decomposition should convince you--you cannot fully reconstruct a vector without information from both the dot and cross products. And as has been said, this product is not commutative.

## Another take on division

Division is typically considered the inverse operation of multiplication. That is to say that if we write 𝑎/𝑏=𝑐, it is the same as 𝑎=𝑏𝑐. If 𝑐 is 𝑎 divided by 𝑏, then 𝑎 is the product of 𝑏 and 𝑐.

When dealing with scalar quantities this is all well and good, but it becomes more complicated when you have objects with different structure, such as vectors. But vectors are kind of like matrices, right? So how does division work there?

Well... it kind of does in some sense, but it kind of doesn't. Instead we consider division to simply be multiplication of a number (or matrix) by its (unique) multiplicative inverse. That is, if 𝑎∈ℝ, then $$ a^{-1} = 1/a $$ is the multiplicative inverse of 𝑎 - or the number such that $$ a a^{-1} = 1 $$. Note that 1 is its own inverse because it is the multiplicative identity. Matrices are not as simple as scalars, but some similarities in how they behave carry through.

Assuming matrix multiplication is familiar to you, we know that any square matrix with nonzero determinant has an inverse, and that the inverse is unique. Multiplication of a matrix 𝐴 by its inverse 𝐴−1 gives the identity matrix, so multiplying any other matrix 𝐵 by 𝐴−1 is sort of the same as "dividing by 𝐴", although in general left- and right-multiplication give different results unless all the matrices involved have special properties.

So this is the matrix equivalent of division. What about vectors?

Well, they're just non-square matrices. One row or one column.

Suppose 𝑢,𝑣 are column vectors in ℝ𝑛. Then the way matrix multiplication normally works we have $$ 𝑢^T𝑣 ∈ ℝ $$ and $$ 𝑢𝑣^𝑇 ∈ ℝ^𝑛 × ℝ^𝑛 $$.

Can we choose for any vector 𝑣 a vector 𝑢 such that 𝑢𝑇𝑣=1?

Well, in terms of the structure of matrix multiplication, this is just the dot product 𝑢⋅𝑣=𝑢1𝑣1+⋯+𝑢𝑛𝑣𝑛. Certainly as long as not all the elements of 𝑣 are zero, we can choose elements of 𝑢 such that it is equal to 1. In fact you'd have infinitely many choices. Consider 𝑛=2. Then, given 𝑣1,𝑣2, we can rearrange 𝑢1𝑣1+𝑢2𝑣2=1 so that $$ 𝑢_2 = \frac{1}{𝑣+2}(1 − 𝑢_1 𝑣_1) $$ is the equation of a line. Any point on that line will satisfy some of the idea of an inverse, but it is not unique.

The other possibility, the dyadic product, $$ 𝑢𝑣^𝑇 = \begin{bmatrix} 𝑢1𝑣1 \\ 𝑢2𝑣1 \\ 𝑢1𝑣2 \\ 𝑢2𝑣2 \end{bmatrix} $$ is more interesting, because it requires that 𝑢1𝑣2=𝑢2𝑣1=0 and 𝑢1𝑣1=𝑢2𝑣2=1. I hope you can see why that's never going to give you an identity matrix given any 𝑣1,𝑣2. Certainly you could not use the same 𝑢 as for the previous scenario.

So with the one way of multiplying two vectors we have a family of multiplicative inverses for a given vector, and the other way we have no multiplicative inverse at all!

It seems that given the way we normally think of multiplying vectors, there's no way of defining a multiplicative inverse of a vector that satisfies the properties we want such an inverse to have.

And that is why division of vectors isn't possible.

## Division

Well… it can be. The problem is that an arbitrary vector space doesn’t naturally come with multiplication.

You can always define multiplication in the naive, component-wise way—e.g.:

(𝑥1,𝑥2,𝑥3)(𝑦1,𝑦2,𝑦3)=(𝑥1𝑦1,𝑥2𝑦2,𝑥3𝑦3).

The problem is that with this notion of multiplication, two non-zero vectors can multiply to zero—e.g.:

(1,0,0)(0,1,0)=(0,0,0).

As a result, you can’t define division—if you try to do so, you will obtain obvious contradictions. (In the preceding example, divide both sides by (0,1,0) —you get (1,0,0)=(0,0,0).)

So, you need to come up with a different notion of multiplication that will avoid such problems. This turns out to be quite difficult.

It is possible for, say, the complex numbers (which you can think of as real vectors with two coordinates), but generally speaking, you shouldn't expect that such a multiplication exists. I wrote more about this here: What prevents the extension of complex numbers to three-dimensional Euclidean space?
https://www.quora.com/What-prevents-the-extension-of-complex-numbers-to-three-dimensional-Euclidean-space

## Division

That's an interesting question. What does "divide" mean? We say that x=a÷b if b•x=a, where "•" is some sort of multiplication. If lots of different "x's" satisfy b•x=a then we can't get a unique result for a÷b. For ordinary numbers, either real or complex, we do have a unique solution x for b•x=a, where "•" is ordinary multiplication, so long as b isn't zero. So we can divide numbers by numbers, as long as we don't divide by zero.

So what sort of "•" could be involved with vectors? The most obvious "•" is the vector dot product, which gives an ordinary number for the dot product of two vectors of the same dimension. The problem is this: if the dimension is two or bigger, you can always find various x's with b•x=0, vectors at right angles to b. You can add those x's to any solution to b•x=a and get other solutions. So there's no unique answer for a÷b where a is a number and b is a vector.

You might wonder about the vector cross product for 3 D vectors, instead of the dot product. We run into a similar problem: any x parallel to b gives (b cross x) = 0, etc.

Now you might get fancier and think about how the product of a matrix and a vector is another vector. You end up with the same problem. If an answer exists, it's not unique.

## Division for Complex Numbers

Josel Cioppa’s answer gives you the mathematical formalism behind this. An example where the multiplication is commutative and invertible is the case of complex numbers. If you have

𝐳1=(𝑎,𝑏)
𝐳2=(𝑐,𝑑)

Then, you have

𝐳1.𝐳2=(𝑎𝑐−𝑏𝑑,𝑎𝑑+𝑏𝑐)

Which you can easily prove is commutative. Also, every non-zero vector in the complex plane is invertible. Note that this also implies that 𝐈=(1,0) is the identity element since

𝐳1.𝐈=(𝑎,𝑏)

We define the multiplicative inverse $$ \vc{z}_1^{-1} $$ of 𝐳1 as the solution to:

𝐳1.𝐳−11=𝐈

It can be seen that the following is a valid definition for $$ \vc{z}_1^{-1} $$:

$$ \vc{z}_1^{-1} = (\frac{a}{a^2+b^2}, -\frac{b}{a^2+b^2}) $$

This can be verified by doing the multiplication. To prove the uniqueness of the $$ \vc{z}_1^{-1} $$, suppose there are two distinct complex vectors 𝐯1 and 𝐯2 that work for $$ \vc{z}_1^{-1} $$.

Then,

𝐳1.(𝐯1−𝐯2)=0⟹𝐯1=𝐯2

We conclude that in the complex plane, the multiplicative inverse of a non-zero complex number is unique.

Among other things, note that defining complex numbers this way is also consistent with (0,1).(0,1)=(−1,0). Also, (𝑎,0).(𝑎,0)=(𝑎^2,0).

# Geometric Algebra Vector Product

https://math.stackexchange.com/questions/3193125/intuition-for-geometric-product-being-dot-wedge-product/3194357?noredirect=1#comment6577962_3194357


Peeter Joot:
Some authors define the geometric product in terms of the dot and wedge product, which are introduced separately. I think that accentuates an apples vs oranges view. Suppose instead you expand a geometric product in terms of coordinates, with $$ \mathbf{a} = \sum_{i = 1}^N a_i \mathbf{e}_i, \mathbf{b} = \sum_{i = 1}^N b_i \mathbf{e}_i $$, so that the product is:

$$ \mathbf{a} \mathbf{b}= \sum_{i, j = 1}^N a_i b_j \mathbf{e}_i \mathbf{e}_j= \sum_{i = 1}^N a_i b_i \mathbf{e}_i \mathbf{e}_i+ \sum_{1 \le i \ne j \le N}^N a_i b_j \mathbf{e}_i \mathbf{e}_j $$

An axiomatic presentation of geometric algebra defines the square of a vector as $$ \mathbf{x}^2 = \left\lVert {\mathbf{x}} \right\rVert^2 $$ (the contraction axiom.). An immediate consequence of this axiom is that $$ \mathbf{e}_i \mathbf{e}_i = 1 $$. Another consequence of the axiom is that any two orthogonal vectors, such as 𝐞𝑖,𝐞𝑗 for 𝑖≠𝑗 anticommute. That is, for 𝑖≠𝑗 :

$$ \mathbf{e}_i \mathbf{e}_j = - \mathbf{e}_j \mathbf{e}_i $$

Utilizing these consequences of the contraction axiom, we see that the geometric product splits into two irreducible portions:

$$ \mathbf{a} \mathbf{b}=\sum_{i = 1}^N a_i b_i+ \sum_{1 \le i < j \le N}^N (a_i b_j - b_i a_j) \mathbf{e}_i \mathbf{e}_j $$

The first sum (the symmetric sum) is a scalar, which we recognize as the dot product 𝐚⋅𝐛, and the second (the antisymmetric sum) is something else. We call this a bivector, or identify it as the wedge product 𝐚∧𝐛.

In this sense, the dot and wedge product sum representation of a geometric product, are just groupings of terms of a larger integrated product.

Another way of reconciling the fact that we appear able to add two unlike entities, is to recast the geometric product in polar form. To do so, consider a decomposition of a geometric product in terms of constituent unit vectors $$ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \hat{\mathbf{a}} \cdot \hat{\mathbf{b}} + \hat{\mathbf{a}} \wedge \hat{\mathbf{b}} } \right) $$, and assume that we are interested in the non-trivial case where 𝐚 and 𝐛 are not colinear (where the product reduces to just $$ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert $$ ). It can be shown that the square of a wedge product is always non-positive, so it is reasonable to define the length of a wedge product like so:

$$ \left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert = \sqrt{-(\hat{\mathbf{a}} \wedge \hat{\mathbf{b}})^2} $$

We can use this to massage the dot plus wedge unit vector sum above into:

$$ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \hat{\mathbf{a}} \cdot \hat{\mathbf{b}} +\frac{\hat{\mathbf{a}} \wedge \hat{\mathbf{b}} }{\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert}\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert} \right) $$

The sum has two scalar factors of interest, the dot product 𝐚̂⋅𝐛̂ and the length of the wedge product $$ \left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert $$. Viewed geometrically, these are the respective projections onto two perpendicular axes, as crudely sketched in the figure "unit circle dot and wedge product components"

That is, we can make the identifications

$$ \hat{\mathbf{a}} \cdot \hat{\mathbf{b}} = \cos\theta $$

$$ \left\lVert { \hat{\mathbf{a}} \wedge \hat{\mathbf{b}} } \right\rVert = \sin\theta $$

Inserting the trigonometric identification of these two scalars into the expansion of the geometric product, we now have

$$ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \cos\theta +\frac{\hat{\mathbf{a}} \wedge \hat{\mathbf{b}} }{\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert}\sin\theta} \right) $$

This has a complex structure that can be called out explicitly by making the identification

$$ \mathbf{i} \equiv\frac{\hat{\mathbf{a}} \wedge \hat{\mathbf{b}} }{\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert} $$

where by our definition of the length of a wedge product $$ \mathbf{i}^2 = -1 $$. With such an identification, we see that the multivector factor of a geometric product has a complex exponential structure

$$ \begin{aligned}\mathbf{a} \mathbf{b}= \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \cos\theta + \mathbf{i} \sin\theta } \right)= \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert e^{\mathbf{i} \theta } \end{aligned} $$

In this view of the geometric product, while we initially added two apparently dissimilar objects, this was really no less foreign than adding real and imaginary portions of a complex number, and we see that the geometric product can be viewed as a scaled rotation operator operating in the plane spanned by the two vectors.

In 3D, the wedge and the cross products are related by what is called a duality relationship, relating a bivector that can be interpreted as an oriented plane, and the normal to that plane. Algebraically, this relationship is

$$ \mathbf{a} \wedge \mathbf{b} = I (\mathbf{a} \times \mathbf{b}) $$

where $$ I = \mathbf{e}_1 \mathbf{e}_2 \mathbf{e}_3 $$ is a unit trivector (often called the 3D pseudoscalar), which also satisfies $$ I^2 = -1 $$. With the usual normal notation for the cross product $$ \mathbf{a} \times \mathbf{b} = \hat{\mathbf{n}} \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \sin\theta $$ we see our unit bivector 𝐢, is related to the cross product normal-direction by $$ \mathbf{i} = I \hat{\mathbf{n}} $$. A rough characterization of this is that 𝐢 is a unit (oriented) plane that is spanned by 𝐚,𝐛 normal to 𝐧̂.

The intuition of that the geometric product and the Lagrange identity are related is on the mark. There is a wedge product generalization of the Lagrange identity in geometric algebra. The 3D form stated in the question follows from the duality relationship of the wedge and cross products.



# TODO

https://math.stackexchange.com/questions/1395970/what-is-the-logic-rationale-behind-the-vector-cross-product

https://math.stackexchange.com/questions/62318/origin-of-the-dot-and-cross-product

https://math.stackexchange.com/questions/1916870/what-is-the-relation-between-quaternions-and-imaginary-numbers/1917093#1917093

https://math.stackexchange.com/questions/185991/is-the-vector-cross-product-only-defined-for-3d

https://math.stackexchange.com/questions/645672/what-is-the-difference-between-a-point-and-a-vector

https://www.quora.com/Why-is-cosine-used-in-dot-products-and-sine-used-in-cross-products

https://www.quora.com/Who-invented-the-dot-product-and-cross-product

https://www.physicsforums.com/threads/dot-product-cross-product-where-did-they-come-from.151710/

https://physics.stackexchange.com/questions/14082/what-is-the-physical-significance-of-dot-cross-product-of-vectors-why-is-divi

https://math.stackexchange.com/questions/180418/calculate-rotation-matrix-to-align-vector-a-to-vector-b-in-3d
