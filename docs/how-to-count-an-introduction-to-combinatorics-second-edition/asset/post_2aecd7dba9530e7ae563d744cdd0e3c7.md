
In this sense every group may be viewed as a group of permutations. However, experience shows that this is not always a helpful way to think about groups. Note also that the group $\langle G^*, \circ \rangle$ generally forms only a small subset of the group $\langle \mathbb{S}(G), \circ \rangle$ of all permutations of the set $G$. For, if $G$ is a group of $n$ elements, there are $n!$ elements in $\mathbb{S}(G)$.

## Exercises

- **11.2.1A** Prove that if $f$ is a symmetry of the figure $F$, then the inverse, $f^{-1}$, of $f$ is also a symmetry of $F$.
- **11.2.1B** Prove that if $f: \mathbb{R}^2 \to \mathbb{R}^2$ is an isometry, then $f$ is surjective.
- **11.2.2A**
    - i. How many symmetries does an equilateral triangle have?
    - ii. Introduce some symbols for the symmetries of an equilateral triangle, and draw up the Cayley table for the group of these symmetries.
    - iii. Express the symmetries of an equilateral triangle as elements of $S_3$ by using the numbers $1, 2,$ and $3$ to label its vertices.
- **11.2.2B**
    - i. How many symmetries does a regular pentagon have?
    - ii. How many symmetries does a regular $n$-gon (that is, a polygon with $n$ sides, with all the sides equal and all the internal angles equal) have?
- **11.2.3A** How many rotational symmetries does a cube have? Describe them.
- **11.2.3B** Investigate the rotational symmetries of a regular tetrahedron.
- **11.2.4A** Show that the group of rotational symmetries of an equilateral triangle is isomorphic to the group of the integers $0, 1, 2$ with addition modulo 3.
- **11.2.4B** Show that every group with two elements is isomorphic to the group $Z_2$ and that every group with three elements is isomorphic to the group $Z_3$.
- **11.2.5A**
    - i. Show that each rectangle has four symmetries (note that we are taking “rectangle” to imply “not a square”) and that the groups of symmetries of any two rectangles are isomorphic. It follows that we can talk about “the group of symmetries of a rectangle.”
    - ii. Show that the group of isometries of a rectangle is not isomorphic to the group $Z_4$.
- **11.2.5B** Prove that every group with four elements is isomorphic to either the group $Z_4$ or to the group of symmetries of a rectangle.

## 11.3 SUBGROUPS AND LAGRANGE'S THEOREM

Group theory is a large subject with an enormous literature. We are going to confine ourselves to those aspects of the subject that are relevant to the combinatorial problems we are interested in. The following definition is important.

### DEFINITION 11.4

Suppose that $G$ is a group. A subset $H$ of $G$ is said to be a **subgroup** of $G$, if $H$ itself forms a group with respect to the same operation that makes $G$ a group.

**Note:** Here it is very convenient to be able to suppress mention of the group operation. If we were being really pedantic, we would have to distinguish between the group operation for $G$, say $*$, which, strictly speaking, is a mapping $* : G \times G \to G$, and the operation on $H$, which is the restriction of $*$ to the set $H$.

Since $H$ is a subset of $G$ and we are using the same operation as for the group $G$, it automatically follows that $H$ satisfies the associativity property. Thus, for $H$ to be a subgroup of $G$, $H$ must be a subset of $G$ that satisfies the following properties, labeled “SG” for “subgroup”.\*

### THE SUBGROUP PROPERTIES

- SG1. $H$ itself is closed under the operation $\bullet$; that is, for all $x$, $y \in H$, $x \bullet y \in H$.
- SG2. $H$ contains the identity element, $e_G$, of $G$.
- SG3. $H$ contains inverses of all its elements; that is, for each $x \in H$, also $x^{-1} \in H$.

We now present some examples of subgroups.

### Examples of Subgroups

1. We have seen that $\mathbb{Z}$, $\mathbb{Q}$, $\mathbb{R}$, and $\mathbb{C}$ are all examples of groups, with the operation of addition in each case. Since $\mathbb{Z} \subseteq \mathbb{Q} \subseteq \mathbb{R} \subseteq \mathbb{C}$, it follows that $\mathbb{Z}$ is a subgroup of $\mathbb{Q}$, $\mathbb{Q}$ is a subgroup of $\mathbb{R}$, and $\mathbb{R}$ is a subgroup of $\mathbb{C}$.

2. Each group, $G$, with more than one element has two *trivial* subgroups. The set $\{e_G\}$ containing just the identity element of $G$ can easily be seen to satisfy the subgroup conditions. At the other extreme, the whole group $G$ also counts as being a subgroup of itself.

3. The eight permutations from $S_4$ corresponding to the symmetries of a square form a subgroup of $S_4$.

4. We consider the group, $S_3$, of all the six permutations of the set $\{1, 2, 3\}$. Rather than write out these permutations in cycle form, we introduce the following symbols for them. We put $p = (1 \ 2 \ 3)$, $q = (1 \ 2)$, $r = (2 \ 3)$, $s = (1 \ 3)$, $t = (2 \ 3)$, and $e$ is the identity element, as usual. The Cayley table for this group is shown in Table 11.3.

It can be seen that the top left-hand corner of the table, taken by itself, is also the Cayley table of a group. In other words the subset $\{e, p, q\}$ forms a subgroup of $S_3$. In this case it is rather easy to spot this. In general, it is rather difficult to find subgroups just by examining Cayley tables. Can you find any more subgroups from this Cayley table? In fact, apart from the two trivial subgroups, and the subgroup $\{e, p, q\}$, there are just three other subgroups, each containing just the identity and one other element.

**TABLE 11.3**

|   | $e$ | $p$ | $q$ | $r$ | $s$ | $t$ |
|---|---|---|---|---|---|---|
| $e$ | $e$ | $p$ | $q$ | $r$ | $s$ | $t$ |
| $p$ | $p$ | $q$ | $e$ | $t$ | $r$ | $s$ |
| $q$ | $q$ | $e$ | $p$ | $s$ | $t$ | $r$ |
| $r$ | $r$ | $s$ | $t$ | $e$ | $p$ | $q$ |
| $s$ | $s$ | $t$ | $r$ | $q$ | $e$ | $p$ |
| $t$ | $t$ | $r$ | $s$ | $p$ | $q$ | $e$ |

> \* See, for example, Allenby, *Rings, Fields and Groups*, Theorem 5.6.5, for a proof that $H$ is a subgroup if and only if it satisfies these subgroup properties.

Some theory comes to our aid when it comes to finding subgroups. This has to do with the number of elements in a subgroup compared with the number of elements in the group. Group theorists have special terminology for the number of elements in a group or a subgroup.

### DEFINITION 11.5

The *order* of a group, or a subgroup, is the number of elements in it.

For example, the order of $S_3$ is 6, and the group of symmetries of a square has order 8. Group theorists often use the notation $o(G)$ for the order of a group, but we have already introduced the notation $\#(G)$ for the number of elements in any set $G$, and so we will keep to this notation.

The key idea in what follows is that given a group $G$ and a subgroup $H$ we can use $H$ to partition $G$ into sets, called, in this context, *cosets*, all having the same number of elements as does $H$. They are defined as follows. To make the general idea more concrete, we use the group $S_3$ as our example.

### DEFINITION 11.6

Let $G$ be a group and let $H$ be a subgroup of $G$. For each $g \in G$, the *coset* $gH$ is defined to be the set $\{gh : h \in H\}$.

We use the notation $gH$ for the coset, as it is obtained by combining the fixed element $g$ of $G$ with all the elements of $H$ in turn, and so the notation $gH$ is rather suggestive and a good aid to memory. We now look at the specific example of the group $S_3$ to make these ideas more concrete.

### PROBLEM 11.1

Find the cosets of the subgroup $\{e, r\}$ of the group $S_3$. (Recall that the Cayley table of $S_3$ is given in Table 11.3.)

### Solution

We calculate the cosets as follows:

$eH = \{ee, er\} = \{e, r\}$,     $qH = \{qe, qr\} = \{q, s\}$,     $sH = \{se, sr\} = \{s, q\}$,

$pH = \{pe, pr\} = \{p, t\}$,     $rH = \{re, rr\} = \{r, e\}$,     $tH = \{te, tr\} = \{t, p\}$.

We see that the cosets of different elements can turn out to be the same set. For example, the cosets $pH$ and $tH$ both consist of the set $\{p, t\}$. Note that as we are dealing with sets, the order in which their elements are listed in our calculation does not matter. In other cases the cosets are completely different. For example, there is no element that is in both $pH$ and $rH$. Thus the different cosets partition $G$ into three disjoint sets, namely, $G = \{e, r\} \cup \{p, t\} \cup \{q, s\}$. Furthermore each coset contains the same number of elements as the subgroup $H$. Thus $\#(G) = 3 \times \#(H)$, and it follows that $\#(H)$ is a divisor of $\#(G)$.
