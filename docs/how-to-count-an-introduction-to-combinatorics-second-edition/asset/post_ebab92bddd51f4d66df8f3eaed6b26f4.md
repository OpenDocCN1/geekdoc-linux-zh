
number by the total number of bridge hands. Thus the required probability is 19,007,345,500/635,013,559,600. This probability is 0.030 to three decimal places.

ii. We need to multiply the answer to Problem 2.9(ii) by the number of ways of choosing the two suits with four cards each and the one suit with three cards, after which the suit with two cards is automatically determined. This multiplier is C(4,2) × C(2,1) = 12. So the total number of such hands is 12 × 11,404,407,300 = 136,852,887,600, and hence the probability of dealing such a hand at random is 136,852,887,600/635,013,559,600, which is 0.216 to three decimal places.

## PROBLEM 2.11

How many poker hands of five cards are there in which there is at least one suit with no cards in it?

### Solution

We list the suit distributions with at least one suit with zero cards in it, and then use the method of Problem 2.10 to work out the total number of hands with these suit distributions, as follows:

| Suit Distribution | Number of Hands |
|---|---|
| 5—0—0—0 | 5,148 |
| 4—1—0—0 | 111,540 |
| 3—2—0—0 | 267,696 |
| 3—1—1—0 | 580,008 |
| 2—2—1—0 | 949,104 |
| Total | 1,913,496 |

You might think that there is a quicker way to solve Problem 2.11. It is easy to count the number of 5-card poker hands with, for example, no spades. Such a hand is obtained by choosing 5 cards from the 39 cards in the pack that are not spades. So there are C(39,5) = 575,757 poker hands with no spades. There is a similar number of hands with no hearts, with no diamonds, and with no clubs, respectively, so it seems that the total number of 5-card hands with a missing suit is 4 × 575,757 = 2,303,028. Unfortunately this quick solution gives an answer that is different from that we obtained in our solution to Problem 2.11. Where have we gone wrong?

It is not difficult to see where our mistake lies. Let $V$ be the set of poker hands with at least one missing suit, and let $V_s, V_h, V_d, V_c$ be those hands with no spades, hearts, diamonds, and clubs, respectively. Clearly, $V = V_s \cup V_h \cup V_d \cup V_c$. Our second calculation assumed that $\#(V) = \#(V_s) + \#(V_h) + \#(V_d) + \#(V_c)$, but this overlooks the fact that some of the hands in $V$ are in more than one of the sets $V_s, V_h, V_d, V_c$. For example, a hand made up of three diamonds and two clubs but no spades and no hearts is in both $V_s$ and $V_h$. Thus the sum $\#(V_s) + \#(V_h) + \#(V_d) + \#(V_c)$ counts some of the hands with a missing suit more than once. Thus it is no wonder that our “quick answer” is higher than the correct answer that we obtained in the solution to Problem 2.11.

To sum up this point, it is correct that if we have a collection of sets $X_1,\ldots,X_k$ that are *pairwise disjoint*, that is, $X_i \cap X_j = \emptyset$ for $1 \le i < j \le k$, then

$$
\#\left(\bigcup_{i=1}^{k} X_i\right) = \sum_{i=1}^{k} \#(X_i), \quad (2.2)
$$

but this is not true if the sets, $X_i$, are not pairwise disjoint. We discuss in Chapter 4 the modification that we need to make to Equation 2.2 in the cases where these sets are not pairwise disjoint.

## Exercises

- **2.4.1A** A ticket wins a fourth prize in the national lottery if precisely four of the six numbers selected on it are included among the six numbers on the balls that are drawn. What is the probability that a ticket wins a fourth prize?

- **2.4.1B** In his autobiography, *What I Remember*, Adolphus Trollope\* describes the Italian lottery as follows:

  > Ninety numbers, 1–90, are always put into the wheel. Five only of these are drawn out. The player bets that a number named by him shall be one of these (*semplece estratto*); or that it shall be the first drawn (*estratto determinato*); or that two numbers named by him shall be two of the five drawn (*ambo*); or that winner of an *estratto determinato*, ought, if the play were quite even, to receive ninety times his stake. But, in fact, such a player would receive only 75 times his stake, the profit of the Government consisting of this pull of 15 per 90 against the player. Of course, what he ought to receive in any of the other cases is easily (not by me, but by experts) calculable.

  What would be fair odds for the *semplece estratto*, *ambo*, and *terno* bets?

- **2.4.2A** A bag contains 50 red balls and 50 blue balls. Ten balls are drawn at random from the bag and not replaced. What is the probability that this sample will contain five red balls and five blue balls? (This question is connected with the reliability of opinion polls. See the solution for more about this.)

- **2.4.2B** A bag contains $2n$ red balls and $2n$ blue balls. What is the probability that if $2n$ balls are drawn at random, the sample will consist of $n$ red balls and $n$ blue balls?

- **2.4.3A** (This is Problem 2B from Chapter 1.) If there are $n$ people in a room, what is the probability that at least two of them share a birthday? How large does $n$ have to be before this probability becomes more than a half? (By “sharing a birthday” we mean that two people were born in the same month and on the same day in that month but not necessarily in the same year. For the purpose of this problem you should ignore leap years, so that there are 365 possible birthdays for each person. You should also assume that all 365 birthdays are equally likely. In fact, as the answer to Exercise 2.4.3B indicates, if, as is actually the case, some birthdays are more likely than others, the probability of a coincidence increases.)

- **2.4.3B** Suppose there are $2n$ balls in a bag of which $a$ are red and $b$ are blue, where $a + b = 2n$. One ball is removed at random from the bag and then replaced. Then a second ball is drawn at random from the bag and then replaced. Calculate the probability that either a red ball is drawn twice or a blue ball is drawn twice. Show that this probability is a minimum when $a = b = n$.

- **2.4.4A** What is the probability that a bridge hand dealt at random has the following suit distributions?
  - i. 5–4–3–1
  - ii. 5–4–4–0
  - iii. 4–3–3–3

- **2.4.4B** Suppose that in a given bridge deal North and South between them have nine spades. What is the probability that the remaining four spades in the other two hands are divided two-two?

- **2.4.5A** *Poker Hands.* Poker hands, which in standard poker games consist of 5 cards drawn from the full pack of 52 cards, are classified as follows:
  - i. *Flush*: five cards all of the same suit but not forming a sequence of consecutive ranks.

    For example, 5♦, 7♦, J♦, Q♦, K♦ is a flush.

  - ii. *Four of a kind*: four cards of one rank and one other card, for example, 3♦, 3♣, 3♥, 3♠, J♦.

  - iii. *Full house*: three cards of one rank and two cards of another rank, for example, 7♦, 7♣, 7♥, 10♦, 10♣.

  - iv. *One pair*: two cards of one rank and three cards of three different ranks, for example, J♦, J♠, 4♦, 7♦, K♦.

  - v. *Straight*: five cards of consecutive ranks but not all in the same suit (note that for this purpose an ace may count either low or high, so that both A, 2, 3, 4, 5 and 10, J, Q, K, A count as consecutive ranks), for example, 7♦, 8♥, 9♣, 10♦, J♠.

  - vi. *Straight flush*: five cards of consecutive ranks (again, an ace may count either low or high) and in the same suit, for example, 4♥, 5♥, 6♥, 7♥, 8♥.

  - vii. *Three of a kind*: three cards of one rank and two cards of two different ranks, for example, 9♦, 9♠, 9♥, 4♦, Q♣.

  - viii. *Two pairs*: two cards of one rank, two cards of another rank, and a fifth card of a third rank, for example, 5♦, 5♠, 8♦, 8♣, J♥.

  - ix. *Other hands*: all other hands that do not fall into any of the preceding categories.

  Calculate how many poker hands there are in each of the categories (a) to (e) above. Hence work out the probability that a poker hand dealt at random falls into each of these categories.

- **2.4.5B** Complete the calculation of Exercise 2.4.5A by working out how many poker hands there are that fall into the categories (f) to (i) above. Also work out the probability that a poker hand dealt at random falls into each of these categories.

- **2.4.6A** We see, from the solution to Problem 2.6, that if a fair coin is tossed 10 times, then the probability of getting four heads is $C(10,4)/2^{10}$. More generally, if a
