that, once the positions of these objects have been chosen, the order in which each object of type \( T_{i} \) is chosen does not matter. Likewise, we need also to divide by \( n_{2}! \), \( n_{3}! \),...,\( n_{k}! \) and hence the number of indistinguishable arrangements is \( n!/(n_{1}!n_{2}!...n_{k}!) \).

# **THEOREM 2.11**
**The Multinomial Theorem**

The coefficient of the term \( a_{1}^{n_{1}}a_{2}^{n_{2}}...a_{k}^{n_{k}} \) in the expansion of \( (a_{1} + a_{2} + ... + a_{k})^{n} \), where \( n_{1} + n_{2} + ... + n_{k} = n \) is \( n!/(n_{1}!n_{2}!...n_{k}!) \).

# Proof

Each term in the expansion of \( (a_{1} + a_{2} + ... + a_{k})^{n} \) has the form \( t_{1}t_{2}...t_{n} \), where each \( t_{r} \), for \( 1 \le r \le n \), is one of the symbols \( a_{1},a_{2},...,a_{k} \). The coefficient of \( a_{1}^{n_{1}}a_{2}^{n_{2}}...a_{k}^{n_{k}} \) is the number of such sequences in which, for \( 1 \le r \le n \), there are \( n_{r} \) occurrences of the symbol \( a_{r} \). By Theorem 2.10 there are \( n!/(n_{1}!n_{2}!...n_{k}!) \) such sequences. This completes the proof.

# Exercises

+   2.5.1A If 12 dice are thrown simultaneously, what is the probability that each of the faces from one to six comes up twice?

+   2.5.1B If 21 dice are thrown simultaneously, what is the probability that 1 comes up once, 2 comes up twice, 3 comes up three times, 4 comes up four times, 5 comes up five times, and 6 comes up six times?

+   2.5.2A In how many different ways can one arrange the sequence of letters in the word ABRACADABRA?

+   2.5.2B In how many different ways can one arrange the sequence of letters in the word PROPERISPOMONON ?

# 2.6 PERMUTATIONS AND CYCLES

In the final section of the chapter, we look at permutations in a new way that will turn out to be very fruitful later on. We have defined a *permutation* of *n* objects to be a way of choosing these objects in order. For example, one permutation of the set \( \{1,2,3,4,5,6\} \) is the choice of these numbers in the order 6,1,3,5,4,2. We can think of this permutation as a reordering of the set.

In this way, we regard this permutation as a bijection (a one-one onto function) mapping the set \( \{1,2,3,4,5,6\} \) to itself. In general, for any set *X*, by a *permutation* of *X*, we mean a bijection \( f: X \to X \). Usually, however, we will be considering permutations of the set \( \{1,2,3,...,n\} \) consisting of the first *n* positive integers.

There are two commonly used notations for permutations. The first is a minor variant of the diagram of Figure 2.4. We drop the arrows and put the numbers inside brackets. So the permutation above would, in this notation, be written as

![](bbox=[0.35, 0.89, 0.65, 0.97])

# FIGURE 2.4