
same as the number of ways of choosing 20 horses in order from a set of 20 horses, and so we could have obtained this by using Theorem 2.1, which tells us that this number is $P(20,20) = 20!/0! = 20!$ (Recall the standard convention that $0! = 1$.) Thus we have:

## **THEOREM 2.2**

The number of different permutations of $n$ objects is $n!$

The values of $n!$ grow very rapidly. Even for quite small values of $n$, the factorial $n!$ is very large. For example, $10! = 3,628,800$ and $100!$ is larger than $10^{457}$.

## **PROBLEM 2.3**

In how many ways can eight counters be placed on a square $8 \times 8$ chessboard in such a way that no two counters lie either in the same row or in the same column? Note that we can reword this problem as: In how many ways can eight rooks be placed on a chessboard so that no two rooks are “attacking” each other? This latter problem is generalized in Chapter 17.

### Solution

Let us place one counter in each row in turn. For the first row there are eight columns in which the counter may be put. Having placed this counter, when it comes to the second row, there are just seven columns where we may place a counter, as it must not be in the same column as the counter in the first row. As we place counters in successive rows, the number of possible columns where the next counter may be placed goes down by one at each stage. So the total number of permissible arrangements of the counters is $8 \times 7 \times \dots \times 2 \times 1$, that is, $8!$ ($= 40,320$). One of these arrangements is shown in Figure 2.2.

Clearly there are, more generally, $n!$ different ways to place $n$ counters on the squares of an $n \times n$ chessboard so that there are neither two counters in the same row nor in the same column. In Exercise 2.2.4A you are asked to generalize this to the case of placing any number of counters on rectangular boards of any size.

![](img/eb401bf41900fd678cd9d368a197e486_36_0.png)

FIGURE 2.2

## Exercises

- **2.2.1A**
  - Currently a €10 note has a "serial number" of the form X19298164502, that is, a letter followed by 11 digits. How many different serial numbers of this form are there? A Bank of England £10 note has a serial number of the form CD49000372, that is, two letters followed by eight digits. Are there more of these serial numbers than there are for a €10 note?

- **2.2.1B**
  - A personal identification number (PIN) consists of a sequence of four digits, each drawn from the set $\{0,1,2,3,4,5,6,7,8,9\}$, except that the first digit of a PIN cannot be 0. How many different PINs are there? How many different PINs are there in which no digit is repeated?

- **2.2.2A**
  - How many different sequences of length 10 are there in which each of the digits $0,1,2,3,4,5,6,7,8,9$ is used once? How long would it take you to list them all if each sequence took one second to write down?

- **2.2.2B**
  - i. How many sequences are there of $n$ digits in which all the digits are different?
  - ii. How many sequences are there of $n$ digits in which no two consecutive digits are the same?

- **2.2.3A**
  - In three races there are 10, 8, and 6 horses running, respectively. You win a jackpot prize if you correctly predict the first 3 horses, in the right order (assuming no dead heats), in each race. How many different predictions can be made?

- **2.2.3B**
  - A password is a sequence of six characters, the first three being either an upper or a lowercase letter, the next being a digit, and the final two coming from the set $\{!,£,\$,\%,\^,\&,\*,(\,),\ldots,\div,\,,\.,\[,],\},\ @,\ \#\,\ ?\}$ of 19 other symbols occurring on a standard keyboard. How many different passwords are there? How many are there if consecutive characters must be different? How many are there if all the characters must be different?

- **2.2.4A**
  - Let $k, m,$ and $n$ be positive integers with $k \leq m$, $k \leq n$, and $m \leq n$. In how many different ways may $k$ counters be placed on the squares of an $m \times n$ grid so that no two counters are in the same row or in the same column?

- **2.2.4B**
  - In how many different ways may eight red and eight green counters be placed on the squares of an $8 \times 8$ chessboard so that there are no two counters on any one square and there is one red counter and one green counter in each row and column?

## 2.3 COMBINATIONS

Let us now count the number of ways of choosing a specified number of objects from a set when the order of selection does not matter. We tackle this problem by relating it to the problem of counting permutations, which we have already solved. (Reducing a new problem to a case that has already been solved is a common mathematical technique. It is said that many a mathematician who has learned how to make a cup of tea starting with an empty kettle will, when given a full kettle and asked to make tea, first empty the kettle to reduce the problem to one that they already know how to solve.) A couple of examples will make the line of approach clear.

## **PROBLEM 2.4**

A team of three bowls players is to be selected from a squad of six players. How many different teams can be selected?

### Solution

We have seen that we can choose three players, in order, from a squad of six players in $P(6, 3)=6 \times 5 \times 4=120$ ways. But, and this is the key point, there are not 120 different teams of three players. This is because the order in which we pick the members of the team does not matter. For example, choosing first Pat, then Chris, and then Sam leads to the same team as first choosing Chris, then Sam, and then Pat. Thus, each team can be chosen in more than one way. The number of ways in which three given players can be chosen in order is $3 !$, that is, 6. Since we get 120 when we count each team six times, the number of different teams is $120/6=20$. Put another way, the number of different ways to pick three bowls players from six is $P(6,3)/3!$

The technique that we have used in this problem is used again, not only in the next problem, but in many other counting problems. We count the number of arrangements of a particular kind by counting them in such a way that each arrangement is counted more than once. We then adjust our answer to allow for the duplicate counting.

## **PROBLEM 2.5**

How many different hands of 5 cards can be chosen from a pack of 52 cards?

### Solution

We can choose 5 cards, in order, from a pack of 52 cards, in $P(52,5)$ different ways. But the order in which the cards are chosen does not affect the hand we end up with. The same hand of 5 cards can be arranged in order in $5 !$ ways and so can be chosen, in order, in $5 !$ ways. Thus $P(52,5)$ gives the number of 5-card hands when each hand is counted $5 !$ times. Hence the number of different 5-card hands is

$$\frac{P(52,5)}{5!} = \frac{(52!/47!)}{5!} = \frac{52!}{5!47!} = \frac{52 \times 51 \times 50 \times 49 \times 48}{5 \times 4 \times 3 \times 2 \times 1} = 2,598,960.$$

We can now generalize the method used in these last two problems. We call a selection of $r$ objects chosen from $n$ objects, when the order in which they are chosen does not matter, a combination of $r$ objects from $n$. We use the notation $C(n,r)$ for the number of different combinations of $r$ objects from $n$. (Notice that the mathematical usage of permutation, where the order matters, and combination, where it does not, does not correspond to all the uses of these words in everyday life. In football pools permutations or "perms" are selections of a football (otherwise known as "soccer") matches where the order does not matter. In a combination lock, the order of the numbers is important.)

The method that we used to solve Problems 2.4 and 2.5 leads us to the general formula for $C(n,r)$.

## **THEOREM 2.3**

For all nonnegative integers $r, n$ with $r \leq n$,

$$C(n, r)=\frac{n !}{r !(n-r) !}.$$

### Proof

By Theorem 2.2, we know that a set of $r$ objects can be ordered in $r !$ ways. Thus $P(n, r)$, the number of ways in which $r$ objects can be chosen in order from a set of $n$ objects, counts each set of $r$ objects chosen from the given set of $r$ objects $r !$ times. Hence, $C(n, r)=P(n, r) / r !$, and therefore, by Theorem 2.1, $C(n, r)=n ! /[r !(n-r) !]$.

The numbers $C(n, r)$ are the well-known binomial coefficients that occur in the binomial theorem that we give as Theorem 2.6. There are several common alternative notations for these binomial coefficients. The number for which we have used the notation $C(n, r)$ is often written as $\binom{n}{r}$, or $_{n} C_{r}$ or $C_{r}^{n}$. We have chosen $C(n, r)$ because it is less cumbersome to print than $\binom{n}{r}$ and, unlike $_{n} C_{r}$ or $C_{r}^{n}$, it makes the numbers $n$ and $r$ easier to read. It also fits in with the standard mathematical notation, $f(x, y)$, for a function of two variables and also with the notation for two-dimensional arrays in many programming languages. Its disadvantage is that it ties the letter $C$ to a particular meaning. To avoid this, the alternative notation $(n r)$ was once suggested.\*

It is worth noting that since $C(n, r)$ is the number of ways of choosing $r$ objects from $n$, we must have $0 \leq r \leq n$. We allow the case $r=n$. In this case the formula gives $C(n, n)=n ! /[0 !(n !)] = 1$. This corresponds to the fact that an $n$-element set $A$ has just one $n$-element subset, namely, the set $A$ itself. We also have $C(n, 0)=n ! /[0 !(n !)] = 1$, corresponding to the fact that there is just one subset of $A$ that has zero elements, namely, the empty set $\varnothing$.

The formula for $C(n, r)$ given by Theorem 2.3 can be used to give algebraic proofs of many properties of the binomial coefficients. We prefer, however, to emphasize the combinatorial meaning of these numbers and to give combinatorial proofs whenever this is convenient. In line with this approach, we have given a combinatorial definition of the number $C(n, r)$. The alternative would have been to define $C(n, r)$ by the formula of Theorem 2.3. It would then have been necessary to prove that the number of $r$-element subsets of an $n$-element set is indeed $C(n, r)$. Our combinatorial approach is illustrated by our proofs of the next four theorems.

## **THEOREM 2.4**

For all positive integers $r, n$ with $r \leq n, r C(n, r)=n C(n-1, r-1)$.

### Proof

Let $X$ be an $n$-element set. We evaluate the sum of the numbers of elements in all the $r$-element subsets of $X$ in two different ways.

\* In *The Printing of Mathematics*, by T. W. Chandy, P. R. Barrett, and Charles Batey, Oxford University Press, London, 1954. This book is out of date technologically as it was written in the days of hot-metal typesetting, but its advice to mathematical authors is still valuable.
