Some theory comes to our aid when it comes to finding subgroups. This has to do with the number of elements in a subgroup compared with the number of elements in the group. Group theorists have special terminology for the number of elements in a group or a subgroup.

# DEFINITION 11.5

The *order* of a group, or a subgroup, is the number of elements in it.

For example, the order of $S_3$ is 6, and the group of symmetries of a square has order 8. Group theorists often use the notation $o(G)$ for the order of a group, but we have already introduced the notation $\#(G)$ for the number of elements in any set $G$, and so we will keep to this notation.

The key idea in what follows is that given a group $G$ and a subgroup $H$ we can use $H$ to partition $G$ into sets, called, in this context, *cosets*, all having the same number of elements as does $H$. They are defined as follows. To make the general idea more concrete, we use the group $S_3$ as our example.

# DEFINITION 11.6

Let $G$ be a group and let $H$ be a subgroup of $G$. For each $g \in G$, the *coset* $gH$ is defined to be the set $\{gh : h \in H\}$.

We use the notation $gH$ for the coset, as it is obtained by combining the fixed element $g$ of $G$ with all the elements of $H$ in turn, and so the notation $gH$ is rather suggestive and a good aid to memory. We now look at the specific example of the group $S_3$ to make these ideas more concrete.

# PROBLEM 11.1

Find the cosets of the subgroup $\{e, r\}$ of the group $S_3$. (Recall that the Cayley table of $S_3$ is given in Table 11.3.)

# Solution

We calculate the cosets as follows:

$eH = \{ee, er\} = \{e, r\}$,     $qH = \{qe, qr\} = \{q, s\}$,     $sH = \{se, sr\} = \{s, q\}$,

$pH = \{pe, pr\} = \{p, t\}$,     $rH = \{re, rr\} = \{r, e\}$,     $tH = \{te, tr\} = \{t, p\}$.

We see that the cosets of different elements can turn out to be the same set. For example, the cosets $pH$ and $tH$ both consist of the set $\{p, t\}$. Note that as we are dealing with sets, the order in which their elements are listed in our calculation does not matter. In other cases the cosets are completely different. For example, there is no element that is in both $pH$ and $rH$. Thus the different cosets partition $G$ into three disjoint sets, namely, $G = \{e, r\} \cup \{p, t\} \cup \{q, s\}$. Furthermore each coset contains the same number of elements as the subgroup $H$. Thus $\#(G) = 3 \times \#(H)$, and it follows that $\#(H)$ is a divisor of $\#(G)$.