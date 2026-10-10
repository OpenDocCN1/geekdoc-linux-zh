240 How to Count: An Introduction to Combinatorics, Second Edition

# **11.4** ORDERS OF GROUP ELEMENTS

Let G be a group, and let g be an element of G. Since G satisfies the closure condition, **gg** is also in G, and hence also g(**gg**), and hence g(g(**gg**)), and so on. Because G satisfies the associativity condition, we can leave out the brackets, and write ggg and gggg for these last two elements of G. At this point it is convenient to introduce the notation g<sup>n</sup> for gggg..., that is, for the result of combining n g's together. Thus g<sup>2</sup> is gg, g<sup>3</sup> is ggg, and so on. We also use g<sup>0</sup> for g, and it will sometimes be convenient to write g<sup>0</sup> for the identity element e. It is immediately apparent that, when m and n are positive integers, g<sup>mn</sup>g<sup>n</sup>=g<sup>m+n</sup>, as both sides of this equation result from combining m+n g's (but note that this index law depends on the associativity property). Also, if g<sup>m</sup>=g<sup>n</sup> with m>n, then g<sup>m</sup>g<sup>−n</sup>g<sup>n</sup>=g<sup>m</sup>, and hence g<sup>m−n</sup>=e. This observation will be useful in the sequel.

Now if G is a finite group, the elements g<sup>n</sup> for n=0,1,2,… cannot all be different. Suppose that g<sup>m</sup>=g<sup>n</sup> with m>n. Then, as we have just noted, g<sup>m−n</sup>=e, where m−n is a positive integer. It follows that there is a smallest positive integer k, such that g<sup>k</sup>=e. This integer k is given a special name.

**DEFINITION 11.7**

The least positive integer, k, if there is one, such that g<sup>k</sup>=e, is called the *order* of the group element g, and is written o(g). If there is no such k, we say that g is *an element of infinite order*.

**PROBLEM 11.2**

Calculate the orders of the elements of the group S<sub>3</sub>, whose Cayley table is given in Table 11.3.

**Solution**

In each group e<sup>1</sup>=e, and so the identity element has order 1. It is, clearly, the only element of order 1. We see from the table that r<sup>2</sup>=s<sup>2</sup>=t<sup>2</sup>=e, and hence g, r, s, and t have order 2. We also have that p<sup>2</sup>=q, and hence p<sup>3</sup>=p(**p**<sup>2</sup>)=pq=e. Thus p≠e, p<sup>2</sup>≠e, but p<sup>3</sup>=e, and so p has order 3. Similarly you can check that q has order 3.

We are now ready to explain the relationship between the meanings of *order* as used in Definitions 11.5 and 11.7. We first need a technical lemma.

**LEMMA 11.7**

Let G be a group and let g be an element of G of (finite) order k. Then for all integers m, n, we have

g<sup>m</sup>=g<sup>n</sup> ⇔ m ≡ n (mod k) (11.4)

and, in particular,

g<sup>n</sup>=e ⇔ n ≡ 0 (mod k); that is, k is a divisor of n. (11.5)