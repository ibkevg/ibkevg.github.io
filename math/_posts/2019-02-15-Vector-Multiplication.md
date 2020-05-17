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
|-|-|-|
| $ a \vc{u} $ | scalar multiplication| vector |  
| $ \vc{u} \cdot \vc{v} $ | dot product (aka scalar product) | scalar |  
| $ \vc{u} \times \vc{v} $ | cross product | vector |  
| $ \inner{\vc u}{\vc v} $ | inner product (~= dot product) | scalar |  
| $ \vc{u} \otimes \vc{v} $ | outer product (aka tensor product) | tensor, multilinear matrix |  
| $ \vc{u} \wedge \vc{v} $ | exterior product (aka wedge product) | bivector |  
| $ \vc{u}\vc{v} = \vc{u} \cdot \vc{v} + \vc{u} \wedge \vc{v} $ | geometric product | multivector |  

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

|Multiplication Property||
|-|-|
Commutative | $ \vc{a}\vc{b} = \vc{b}\vc{a} $
Associative | $ \vc{a}(\vc{b}\vc{c}) = (\vc{a}\vc{b})\vc{c} $  
Distributive | $ \vc{a} (\vc{b} + \vc{c} ) = \vc{a}\vc{b} + \vc{a}\vc{c} $
Identity (Note that this is required for division to exist.) | $ 1\vc{a} = \vc{a} $ 
Inverse (or reciprocal) | $ \vc{a} \vc{a}^{-1} = \vc{a}^{-1} \vc{a} = 1 $


Many of these seem like they're stating the obvious, however its useful to be explicit when listing requirements.

**Supports Division**

When we say we want division to exist and work for vectors the same as it does for regular numbers, we again mean we want them to support the same set of properties.

|Division Property|||
|-|-|-|
Not commutative| $ \vc{a} \div \vc{b} \neq \vc{b} \div \vc{a} $| $ \frac{\vc{a}}{\vc{b}} \ne \frac{\vc{b}}{\vc{a}} $
Not associative| $ \vc{a} \div (\vc{b} \div \vc{c}) \neq (\vc{a} \div \vc{b}) \div \vc{c} $ | $ \frac{\vc{a}\vc{c}}{\vc{b}} \ne \frac{\vc{a}}{\vc{b}\vc{c}} $
Not left distributive | $ \vc{c} \div (\vc{a}+\vc{b}) \ne (\vc{c} ÷ \vc{a}) + (\vc{c} ÷ \vc{b}) $ | $ \frac{\vc{c}}{\vc{a} + \vc{b}} \ne \frac{\vc{c}}{\vc{a}} + \frac{\vc{c}}{\vc{b}} $
But is right distributive | $ (\vc{a}+\vc{b}) ÷ \vc{c} = (\vc{a} ÷ \vc{c}) + (\vc{b} ÷ \vc{c}) $ | $ \frac{\vc{a} + \vc{b}}{\vc{c}} = \frac{\vc{a}}{\vc{c}} + \frac{\vc{b}}{\vc{c}} $

**Regular number multiplication is just a special case**

It would be beautiful if ordinary regular number multiplcation fell out of our new vector/vector product as a special case.

**Closed under multiplication**

Ideally, we hope that multiplying two vectors would result in another vector, just the same as happens when multiplying reals or complex numbers.

## Division

In order to support division we need to be able to be able to take the result of a dot product and recover one of the original vectors by dividing out the other. For this we need the properties below.

We need a multiplicative identity:

$$ 1 \cdot \vc{u} = \vc{u} $$

We need a multiplicative inverse:

$$ \vc{v} \cdot \vc{v}^{-1} = 1 $$

If we can make those work we can define division as dotting with an inverse.

$$ \frac{\vc{a}}{\vc{b}} = \vc{a} \cdot \vc{b}^{-1} = \vc{c} $$

A scalar value of 1 works just fine for an identity but we run into a problem when we try to define the inverse of a vector. The dot product loses all directionality information and so recovering an input vector, including it's direction is impossible.


# Geometric Algebra

The big idea of geometric algebra (aka Clifford Algebra) is to explicitly define vector multiplication in the following way:

$$ \vc{a} \vc{b} = \vc{a} \cdot \vc{b} + \vc{a} \wedge \vc{b} $$

Think of the sum as like the real and imaginary parts of a complex number.


## Division

The question "what does $ \vc{a} / \vc{b} $ equal?" is equivalent to asking "What do you multiply with $ \vc{b} $ to get $ \vc{a} $?"

How would you define the inverse of a vector such that $ \vc{v}\vc{v}^{-1} = 1 $? What would be the "identity vector" 1

In fact, the answer is sometimes you can. In particular, in two dimensions, you can make a correspondence between vectors and complex numbers, where the real and imaginary parts of the complex number give the (x,y) coordinates of the vector. Division is well-defined for the complex numbers.

The cross-product only exists in 3D.

Division is defined in some higher-dimensional spaces too (such as the quaternions), but only if you give up commutativity and/or associativity.

For ordinary numbers, I think of $ x/y $ as being the number that, when multiplied by $ y $, gives $ x $. So, $ \vc{x} / \vc{y} $ would have to be the vector that, when "multiplied" by $ \vc{y} $, gives $ \vc{x} $. If our multiplication involves the dot product, we're already in trouble, because the dot product of two vectors is a scalar, and the definition above would therefore require $ \vc{x} / \vc{y} $ to simultaneously be a vector and a scalar.

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

Well... it kind of does in some sense, but it kind of doesn't. Instead we consider division to simply be multiplication of a number (or matrix) by its (unique) multiplicative inverse. That is, if 𝑎∈ℝ, then $ a^{-1} = 1/a $ is the multiplicative inverse of 𝑎 - or the number such that $ a a^{-1} = 1 $. Note that 1 is its own inverse because it is the multiplicative identity. Matrices are not as simple as scalars, but some similarities in how they behave carry through.

Assuming matrix multiplication is familiar to you, we know that any square matrix with nonzero determinant has an inverse, and that the inverse is unique. Multiplication of a matrix 𝐴 by its inverse 𝐴−1 gives the identity matrix, so multiplying any other matrix 𝐵 by 𝐴−1 is sort of the same as "dividing by 𝐴", although in general left- and right-multiplication give different results unless all the matrices involved have special properties.

So this is the matrix equivalent of division. What about vectors?

Well, they're just non-square matrices. One row or one column.

Suppose 𝑢,𝑣 are column vectors in ℝ𝑛. Then the way matrix multiplication normally works we have $ 𝑢^T𝑣 ∈ ℝ $ and $ 𝑢𝑣^𝑇 ∈ ℝ^𝑛 × ℝ^𝑛 $.

Can we choose for any vector 𝑣 a vector 𝑢 such that 𝑢𝑇𝑣=1?

Well, in terms of the structure of matrix multiplication, this is just the dot product 𝑢⋅𝑣=𝑢1𝑣1+⋯+𝑢𝑛𝑣𝑛. Certainly as long as not all the elements of 𝑣 are zero, we can choose elements of 𝑢 such that it is equal to 1. In fact you'd have infinitely many choices. Consider 𝑛=2. Then, given 𝑣1,𝑣2, we can rearrange 𝑢1𝑣1+𝑢2𝑣2=1 so that $ 𝑢_2 = \frac{1}{𝑣+2}(1 − 𝑢_1 𝑣_1) $ is the equation of a line. Any point on that line will satisfy some of the idea of an inverse, but it is not unique.

The other possibility, the dyadic product, $ 𝑢𝑣^𝑇 = \begin{bmatrix} 𝑢1𝑣1 \\ 𝑢2𝑣1 \\ 𝑢1𝑣2 \\ 𝑢2𝑣2 \end{bmatrix} $ is more interesting, because it requires that 𝑢1𝑣2=𝑢2𝑣1=0 and 𝑢1𝑣1=𝑢2𝑣2=1. I hope you can see why that's never going to give you an identity matrix given any 𝑣1,𝑣2. Certainly you could not use the same 𝑢 as for the previous scenario.

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

$$
𝐳1=(𝑎,𝑏)
𝐳2=(𝑐,𝑑)
$$

Then, you have

$$ 𝐳1.𝐳2=(𝑎𝑐−𝑏𝑑,𝑎𝑑+𝑏𝑐) $$

Which you can easily prove is commutative. Also, every non-zero vector in the complex plane is invertible. Note that this also implies that 𝐈=(1,0) is the identity element since $ 𝐳1.𝐈=(𝑎,𝑏) $

We define the multiplicative inverse $ \vc{z}_1^{-1} $ of 𝐳1 as the solution to:

𝐳1.𝐳−11=𝐈

It can be seen that the following is a valid definition for $ \vc{z}_1^{-1} $:

$$ \vc{z}_1^{-1} = (\frac{a}{a^2+b^2}, -\frac{b}{a^2+b^2}) $$

This can be verified by doing the multiplication. To prove the uniqueness of the $ \vc{z}_1^{-1} $, suppose there are two distinct complex vectors 𝐯1 and 𝐯2 that work for $ \vc{z}_1^{-1} $.

Then,

𝐳1.(𝐯1−𝐯2)=0⟹𝐯1=𝐯2

We conclude that in the complex plane, the multiplicative inverse of a non-zero complex number is unique.

Among other things, note that defining complex numbers this way is also consistent with (0,1).(0,1)=(−1,0). Also, (𝑎,0).(𝑎,0)=(𝑎^2,0).

# Geometric Algebra Vector Product

https://math.stackexchange.com/questions/3193125/intuition-for-geometric-product-being-dot-wedge-product/3194357?noredirect=1#comment6577962_3194357


Peeter Joot:
Some authors define the geometric product in terms of the dot and wedge product, which are introduced separately. I think that accentuates an apples vs oranges view. Suppose instead you expand a geometric product in terms of coordinates, with $ \mathbf{a} = \sum_{i = 1}^N a_i \mathbf{e}_i, \mathbf{b} = \sum_{i = 1}^N b_i \mathbf{e}_i $, so that the product is:

$$ \mathbf{a} \mathbf{b}= \sum_{i, j = 1}^N a_i b_j \mathbf{e}_i \mathbf{e}_j= \sum_{i = 1}^N a_i b_i \mathbf{e}_i \mathbf{e}_i+ \sum_{1 \le i \ne j \le N}^N a_i b_j \mathbf{e}_i \mathbf{e}_j $$

An axiomatic presentation of geometric algebra defines the square of a vector as $ \mathbf{x}^2 = \left\lVert {\mathbf{x}} \right\rVert^2 $ (the contraction axiom.). An immediate consequence of this axiom is that $ \mathbf{e}_i \mathbf{e}_i = 1 $. Another consequence of the axiom is that any two orthogonal vectors, such as 𝐞𝑖,𝐞𝑗 for 𝑖≠𝑗 anticommute. That is, for 𝑖≠𝑗 :

$$ \mathbf{e}_i \mathbf{e}_j = - \mathbf{e}_j \mathbf{e}_i $$

Utilizing these consequences of the contraction axiom, we see that the geometric product splits into two irreducible portions:

$$ \mathbf{a} \mathbf{b}=\sum_{i = 1}^N a_i b_i+ \sum_{1 \le i < j \le N}^N (a_i b_j - b_i a_j) \mathbf{e}_i \mathbf{e}_j $$

The first sum (the symmetric sum) is a scalar, which we recognize as the dot product 𝐚⋅𝐛, and the second (the antisymmetric sum) is something else. We call this a bivector, or identify it as the wedge product 𝐚∧𝐛.

In this sense, the dot and wedge product sum representation of a geometric product, are just groupings of terms of a larger integrated product.

Another way of reconciling the fact that we appear able to add two unlike entities, is to recast the geometric product in polar form. To do so, consider a decomposition of a geometric product in terms of constituent unit vectors $ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \hat{\mathbf{a}} \cdot \hat{\mathbf{b}} + \hat{\mathbf{a}} \wedge \hat{\mathbf{b}} } \right) $, and assume that we are interested in the non-trivial case where 𝐚 and 𝐛 are not colinear (where the product reduces to just $ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert $ ). It can be shown that the square of a wedge product is always non-positive, so it is reasonable to define the length of a wedge product like so:

$$ \left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert = \sqrt{-(\hat{\mathbf{a}} \wedge \hat{\mathbf{b}})^2} $$

We can use this to massage the dot plus wedge unit vector sum above into:

$$ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \hat{\mathbf{a}} \cdot \hat{\mathbf{b}} +\frac{\hat{\mathbf{a}} \wedge \hat{\mathbf{b}} }{\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert}\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert} \right) $$

The sum has two scalar factors of interest, the dot product 𝐚̂⋅𝐛̂ and the length of the wedge product $ \left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert $. Viewed geometrically, these are the respective projections onto two perpendicular axes, as crudely sketched in the figure "unit circle dot and wedge product components"

That is, we can make the identifications

$$ \hat{\mathbf{a}} \cdot \hat{\mathbf{b}} = \cos\theta $$

$$ \left\lVert { \hat{\mathbf{a}} \wedge \hat{\mathbf{b}} } \right\rVert = \sin\theta $$

Inserting the trigonometric identification of these two scalars into the expansion of the geometric product, we now have

$$ \mathbf{a} \mathbf{b} = \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \cos\theta +\frac{\hat{\mathbf{a}} \wedge \hat{\mathbf{b}} }{\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert}\sin\theta} \right) $$

This has a complex structure that can be called out explicitly by making the identification

$$ \mathbf{i} \equiv\frac{\hat{\mathbf{a}} \wedge \hat{\mathbf{b}} }{\left\lVert {\hat{\mathbf{a}} \wedge \hat{\mathbf{b}}} \right\rVert} $$

where by our definition of the length of a wedge product $ \mathbf{i}^2 = -1 $. With such an identification, we see that the multivector factor of a geometric product has a complex exponential structure

$$ \begin{aligned}\mathbf{a} \mathbf{b}= \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \left( { \cos\theta + \mathbf{i} \sin\theta } \right)= \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert e^{\mathbf{i} \theta } \end{aligned} $$

In this view of the geometric product, while we initially added two apparently dissimilar objects, this was really no less foreign than adding real and imaginary portions of a complex number, and we see that the geometric product can be viewed as a scaled rotation operator operating in the plane spanned by the two vectors.

In 3D, the wedge and the cross products are related by what is called a duality relationship, relating a bivector that can be interpreted as an oriented plane, and the normal to that plane. Algebraically, this relationship is

$$ \mathbf{a} \wedge \mathbf{b} = I (\mathbf{a} \times \mathbf{b}) $$

where $ I = \mathbf{e}_1 \mathbf{e}_2 \mathbf{e}_3 $ is a unit trivector (often called the 3D pseudoscalar), which also satisfies $ I^2 = -1 $. With the usual normal notation for the cross product $ \mathbf{a} \times \mathbf{b} = \hat{\mathbf{n}} \left\lVert {\mathbf{a}} \right\rVert \left\lVert {\mathbf{b}} \right\rVert \sin\theta $ we see our unit bivector 𝐢, is related to the cross product normal-direction by $ \mathbf{i} = I \hat{\mathbf{n}} $. A rough characterization of this is that 𝐢 is a unit (oriented) plane that is spanned by 𝐚,𝐛 normal to 𝐧̂.

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
