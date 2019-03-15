
TODO


## Multiplying Complex Numbers

One source of potential insight are complex numbers because they are, in a sense, vectors. For example, you might think of the real and imaginary parts as X and Y coordinates.

So how do we multiply complex numbers?

$$
\begin{aligned}
(a + b\ihat)(c + d\ihat)
&= ac + ad\ihat + bc\ihat + bd\ihat\ihat \\
&= (ac - bd) + (ad + bc)\ihat
\end{aligned}
$$


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



# Geometric Algebra vs Matricies

https://math.stackexchange.com/questions/468532/in-geometric-algebra-is-there-a-geometric-product-between-matrices


# What can complex numbers do that linear algebra cannot?

Aren't complex numbers basically the same as 2 dimensional linear algebra?


The next crucial stage of the story occurs in 1878 with the work of the English mathematician, William Kingdon Clifford (Clifford 1878). Clifford was one of the few mathematicians who had read and understood Grassmann's work, and in an attempt to unite the algebras of Hamilton and Grassmann into a single structure, he introduced his own geometric algebra. In this algebra we have a single geometric product formed by uniting the inner and outer products—this is associative like Grassmann's product but also invertible, like products in Hamilton's algebra. In Clifford's geometric algebra an equation of the type 𝐚𝐛=𝐶 has the solution 𝐛=𝐚^−1𝐶, where 𝐚^−1 exists and is known as the inverse of a. Neither the inner or outer product possess this invertibility on their own. Much of the power of geometric algebra lies in this property of invertibility.

The key point is that the geometric product can take 1 as its multiplicative identity and hence define inverses with respect to 1 being that identity. Neither the dot nor wedge products have a meaningful multiplicative identity, so you can't say that the inversion only uses one or the other.



https://math.stackexchange.com/questions/443475/whats-the-motivation-to-add-inner-product-and-wedge-product-together-in-geometr
It isn't so much that the Clifford product is useful as that it's natural.

Instead of defining the Clifford product as 𝑣⋅𝑤+𝑣∧𝑤 , you can define the Clifford algebra as the algebra in which S+S and V+V addition, SS and SV multiplication, and V2 squared norm have their usual meanings from vector calculus, the usual algebraic rules apply (except for commutativity of multiplication), and there are no other constraints. It isn't obvious that this produces anything sensible, but if it does (and indeed it does) then it seems quite natural. Starting from that formulation, the identity 𝑣⋅𝑤=1/2(‖𝑣+𝑤‖^2−‖𝑣‖^2−‖𝑤‖^2) gives you 𝑣⋅𝑤=1/2(𝑣𝑤+𝑤𝑣), and you can show that 1/2(𝑣𝑤−𝑤𝑣) satisfies all of the axioms of the wedge product, which justifies calling it 𝑣∧𝑤, and adding those together yields 𝑣𝑤=𝑣⋅𝑤+𝑣∧𝑤.

You could also informally motivate the sum by the fact that |𝑣⋅𝑤|^2=‖𝑣‖^2‖𝑤‖^2cos^2𝜃 and ‖𝑣∧𝑤‖^2=‖𝑣‖^2‖𝑤‖^2sin^2𝜃, so it makes sense to combine them to get a product that satisfies ‖𝑣𝑤‖^2=‖𝑣‖^2‖𝑤‖^2 yet also preserves 𝜃 by putting the inner and wedge products in orthogonal components of the result. Straying further into truthiness-based argument, the wedge product is also called the (Grassmann) exterior product, and the (Grassmann) interior product coincides with the inner product for vectors, so you can say that the Clifford product combines the interior and exterior Grassmann products. They sound like they belong together, at least.



# Why both dot and cross product?

The dot product gives you the multiplication of the parallel components.

Example: The torque expression, $$ \vec{\tau} = \vec{F} \times \vec{r} $$, where only the force component perpendicular to the "arm" (or likewise vise versa) is wanted.

Why cant we just have dot product? Simply because we sometimes want the perpendicular variation and not only the parallel one. At some point the cross product was "invented" to describe this in a neat and concise expression.

# Why Vector product have direction and not for Dot product?

Just keep in mind that while the dot product (or scalar product) gives you a number only (a scalar), the cross product (or vector product) gives you a number with a direction (that is, a vector). And this direction is perpendicular to both.

@ibsenv The scalar product represents length and angles, so it must have scalar value to extract the information. It is not obvious from elementary definitions, but if you "arrive at" the cross product from some higher mathematics approach (exterior algebra, Lie-groups), it either represents oriented area elements or infinitesimal rotations. In 3-space both have exactly 3 degrees of freedom, thus the set of oriented area elements or infinitesimal rotations can be identified with ℝ3 itself, hence the vectorial value. – Bence Racskó May 26 '15 at 9:48 

@ibsenv You can either see Uldreth's comment, or you can consider it as "just a convention". In the first example above (the dot product) there is no need for the orientation, as the result is along both vectors. In the second example (with torque) you are "turning" around an axis. It makes sense that this axis is perpendicular to both original vectors, and by defining the cross product in this way, this axis direction can simply be calculated directly as a vector. – Steeven May 26 '15 at 13:50 

@Uldreth, Steevan, so If I understand correctly,In simple words Vector product is just another version of dot product, where your output is also a vector quantity. Both are used for comparing two 2 vectors. There is no other difference. Am I right? – ibsenv May 28 '15 at 4:52

@Steeven, Uldreth, Can I even say dot products are simply a subset of vector products with the direction practically meaningless or same relative to the direction of interest. (So we ignore the direction and call it scalar)? – ibsenv May 28 '15 at 4:59

@ibsenv Hmm, not really. I can't really explain this in such a short space, but you really should not look at /any/ "product" on a vector space as a natural operation. Some vector spaces admit 'proper' products, we call these algebras. For other vector spaces, we have tensor and exterior products that are natural, but they are not product operations on the space, but rather on the tensor/exterior algebras of the space. Those are best viewed as a most general representation of multilinear functions on the vector space, rather than a product. – Bence Racskó May 28 '15 at 7:03

@ibsenv The 'dot' product is not a product by any means, actually. The cross product is a 'proper' product operation, but it is not 'natural' either. The cross product depends on 1) the dot product; 2) the orientation of the space; 3) the 3-dimensionality of the space. It is a representation of the exterior product, that can only be made if the above three conditions are satisfied. So in essence, the cross product 'depends on' the 'dot product', but it is absolutely not "another version" of the dot product. – Bence Racskó May 28 '15 at 7:06



## Dot Product Notes

(i) $$ \vec{A} \cdot \vec{B} = \vec{B} \cdot \vec{A} $$

(ii) $$ \vec{A} \cdot (\vec{B} + \vec{C}) = \vec{A} \cdot \vec{B} + \vec{A} \cdot \vec{C} $$

(iii) $$ \sqrt{\vec{A} \cdot \vec{A}} = \lvert \vec{A} \rvert $$

(iv) $$ \vec{A} \cdot \vec{B} = A(B \cos \theta) = \text{A times the component of B along A} $$

or $$ \vec{A} \cdot \vec{B} = B(A \cos \theta) = \text{ B times the component of A along B} $$

(v) $$ \ihat \cdot \ihat = \jhat \cdot \jhat = \khat \cdot \khat = (1)(1)\cos 0 = 1 $$

(vi) $$ \ihat \cdot \jhat = \ihat \cdot \khat = \jhat \cdot \khat = (1)(1)\cos 90^\circ = 0 $$

(vii) $$
\begin{align}
\vec{u} \cdot \vec{v}
&= 
\begin{pmatrix} u_x \ihat + u_y \jhat + u_z \khat \end{pmatrix} \cdot
\begin{pmatrix} v_x \ihat + v_y \jhat + v_z \khat \end{pmatrix} \\
&= u_x v_x + u_y v_y + u_z v_z
\end{align}
$$

(viii) $$ \theta = \arcsin \frac{\vec{A} \cdot \vec{B}}{AB} $$

(ix) Two vectors are perpendicular if their dot product is 0 (i.e. $$\theta=90^\circ$$)

When dealing with geometric algorithms, you usually end up using a lot of dot and cross products. For example:

* Dot product let you easily and quickly check if two vectors are perpendicular, or the angle between them (well, to be precise, the cosine of their angle, but having directly the cosine of an angle is sometimes better than having the angle itself). Also, the dot product of a vector with a base vector is the coordinate of this vector in the base along the vector axis, it’s useful for example to compute coordinates in another base.
* Cross product will give you a vector that is normal to the plane defined by two vectors, or can be used to determine if two vectors are co-linear (their cross product is zero).
The main advantages of dot and cross products is that they are quick to compute on a general computer (a few multiplications and additions), and that their formula are very easy.

Why cos(θ) ?

OK, to multiply two vectors it makes sense to multiply their lengths together but only when they point in the same direction. So we make one "point in the same direction" as the other by multiplying by cos(θ)

Dot products are also handy because they provide a way to find the angle between two vectors.

## References
https://math.stackexchange.com/questions/348717/dot-product-intuition
http://vmls-book.stanford.edu/vmls.pdf#page29
https://www.cc.gatech.edu/~jarek/graphics/reading/geometry2D.pdf
https://www.cc.gatech.edu/~jarek/graphics/reading/?C=S;O=A
https://www.quora.com/Why-is-cosine-used-in-dot-products-and-sine-used-in-cross-products

# Cross Product
Let's first motivate the cross product using torque.

Let's say we have a screw, $$ a $$ which we will drive using a wrench. The length of the wrench is $$ d $$ and we apply a force $$ F $$ at the end of the wrench perpendicular to the shaft. We find that the torque $$ \tau $$ about point $$ a $$ is:

$$ \tau_a = l F $$

Now what if the force is not applied perfectly perpendicular to the wrench but instead is slightly at an angle $$ \theta $$?

Here we find that only the component of the force that is perpendicular to the wrench contributes to the torque and the component that is parallel to the wrench simple pushes on the screw and offers no turning power. Mathematically this is:

$$
\begin{align}
\tau_a &= l \left\lVert F \right\rVert \cos {\theta} \\
       &= \vec l \times \vec F
\end{align}
$$

# References

* http://behindtheguesses.blogspot.com/2009/04/dot-and-cross-products.html
* https://www.physicsforums.com/threads/dot-product-cross-product-where-did-they-come-from.151710
* https://www.quora.com/Why-is-the-definition-of-the-dot-product-the-way-it-is
* https://www.quora.com/Who-invented-the-dot-product-and-cross-product
* http://math.ucv.ro/~niculescu/articles/2012/LagrangeApril12.pdf
* http://vmls-book.stanford.edu/vmls.pdf

# Misc

$$
\begin{align}
\vec u &= \langle x, y, z \rangle  \\
       &= x \ihat + y \jhat + z \khat  \\
\end{align}
$$


Cross Product produces a "pseudo vector" not a real vector.
* https://en.wikipedia.org/wiki/Pseudovector
