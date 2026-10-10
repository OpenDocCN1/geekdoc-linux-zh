![](bbox=[0.15, 0.08, 0.5, 0.28])

> **The symmetries of a square**
> * e Identity
> * a Rotation through 1/2 clockwise
> * b Rotation through π clockwise
> * c Rotation through 1/2 anticlockwise
> * h Reflection in the horizontal axis
> * v Reflection in the vertical axis shown
> * r Reflection in the diagonal axis shown
> * s Reflection in the diagonal axis shown
> 
> The rotations are about the axis through the *centre* of the square and perpendicular to it.

FIGURE 11.2

This is nothing more than our usual stipulation that if *f* : *D* → *C* and *g* : *D* → *C* are both functions with the same domain and codomain and for all *x* ∈ *D*, *f*(*x*) = *g*(*x*) then we say that *f* = *g*.

Now that we have been careful to say what we mean by a symmetry of a figure we can see that a square has eight symmetries, as shown in Figure 11.2. The symbols used for these symmetries are somewhat arbitrary, but we will continue to use them.

We will use the notation S(⊕) for the group of symmetries of a square. It is now quite straightforward to work out the Cayley table for this group. We encourage you to do this. You might find it helpful to have an actual square to manipulate. Don’t forget that in line with our usual convention for composing functions, when we compose two symmetries, say *f* and *g*, to obtain the composite *fg* this means *first do g, then do f*.

You should obtain exactly the same table as Table 11.2 in the previous section. Since the operation is composition of functions, we now know, without having to do lots of calculations, that the operation defined by Table 11.2 is associative. Hence it is the Cayley table of a group. In particular, we can also deduce that the symmetries of a square form a group. This is a special case of the more general result that the symmetries of any figure always form a group. This we now prove.

# THEOREM 11.2

The set, *G*, of the symmetries of a figure, *F*, with the operation, denoted by ⊙, of composition, forms a group.

# **Proof**

We need to check that the four group properties are satisfied by (*G*, ⊙). Suppose that *f* and *g* are symmetries of *F*. Then as *f* and *g* are both isometries we have, for all points *p* and *q* (of the appropriate space),

```
d(*fg*(*p*), *fg*(*q*)) = d(*f*(*g*(*p*)), *f*(*g*(*q*))) = d(*g*(*p*), ⋈*g*(*q*)) = d(*p*,*q*),
```