![](bbox=[0.35, 0.13, 0.65, 0.25])

FIGURE 4.1

# PROBLEM 4.1

How many integers are there in the range from 1 to 1,000,000 that are divisible by 2 or 3 or both?

# Solution

We let $D_2$ and $D_3$ be the sets of those integers in the range from 1 to 1,000,000 that are divisible by 2 and by 3, respectively. By Theorem 4.1, #$(D_2 \cup D_3)$ = #$(D_2)$ + #$(D_3)$ – #$(D_2 \cap D_3)$. Clearly, #$(D_2)$ = 500,000 and #$(D_3)$ = 333,333. Now, an integer is divisible by both 2 and 3 if and only if it is divisible by 6. Hence #$(D_2 \cap D_3)$ = 166,666. Therefore #$(D_2 \cup D_3)$ = 500,000 + 333,333 – 166,666 = 666,667.

Theorem 4.1 can easily be extended to deal with the case of three sets. All we need do is to write $A \cup B \cup C$ as $(A \cup B) \cup C$ and then apply Theorem 4.1, making use of some elementary set algebra. This gives

```
#$(A \cup B \cup C)$ = #($((A \cup B) \cup C)$)
		= #$(A \cup B)$ + #$(C)$ – #($((A \cup B) \cap C)$)
		= (##$(A)$ + ##$(B)$ – #$(A \cap B)$) + #$(C)$ – ((#$(A) \cup #B$) \cap #$(C)$),
```

using Theorem 4.1 twice. Now, by the distributive law for unions and intersections of sets, $(A \cup B) \cap C$ = $(A \cap C) \cup (B \cap C)$. Hence, using Theorem 4.1 again,

```
#($((A \cup B) \cap C)$) = #$(A \cap C)$ + #$(B \cap C)$ – #($((A \cap C) \cap (B \cap C)$),
```

and therefore, as $(A \cap B) \cap (B \cap C)$ = $A \cap B \cap C$, we deduce that

```
#$(A \cup B \cup C)$ = (##$(A)$ + ##$(B)$ + ##$(C)$) – (##$(A \cap B)$ + ##$(A \cap C)$ + ##$(B \cap C)$) + #$(A \cap B \cap C)$.
```

Now let us see what this formula means. The three terms in the first pair of brackets count the members of $A$, $B$, and $C$ separately. Thus, when we add them up, we have counted elements that are in two of the sets twice, and those in all three are counted three times. We take account of this double counting by subtracting the terms in the second pair of brackets. However, when we do this, an element that is in all three of the