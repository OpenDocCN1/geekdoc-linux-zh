possible outcomes are \( E_1, \dots, E_n \) and that whenever \( E_i \) occurs the conditional probability \( E'_j \) of the next trial is \( p_{ij} \), independent of what happened at the preceding trials. Here, of course, \( p_{ij} \ge 0 \) and \( p_{i1} + p_{i2} + \dots + p_{in} = 1 \) for each \( i \). They are called transition probabilities. The whole process is now determined if the initial probabilities \( \pi_i \), at the first trial are known. For example, \( P(E_1 E_2 E_3) = \pi_1 p_{12} p_{23} \). The probability of the event \( “E_n \) at the third trial” is obtained by summation over all a and b, and so on. Markov chains, and their analog with continuing time, represent the simplest type of stochastic process. See STOCHASTIC PROCESS.

# **Random variables and their distributions.**

The theory of probability traces its origin to gambling, and the gambler’s gain may still serve as the simplest example of a random variable.

With every possible outcome (sample point) there is associated a number, namely, the corresponding gain. In other words, the gain is a function on the sample space, and such functions are called random variables. With the same experiment, one may associate many random variables.

Every random variable X has a distribution function F(t) = P(X \le t). If X assumes only finitely many values, then F(t) is a step function. The notion of independence carries over: Two random variables X and Y are independent if P(X \le x, Y \le y) = P(X \le x) \cdot P(Y \le y).

# **Expectations.**

Given a random variable X one may interpret its distribution function F(t) as describing the distribution of a unit mass along the real axis such that the interval \( a < x \le b \) carries mass \( F(b) - F(a) \). In the case of a discrete variable assuming the values \( x_1, x_2, \dots \), with probabilities \( p_1, p_2, \dots \), the entire mass is concentrated at the points \( x_i \); if \( F(x) = F(x) \) exists, it represents the ordinary mass density as defined in \(\cdot\cdot\cdot\). The center of gravity of this mass distribution is called the expectation of X, the usual symbol for it is \( E(X) \), but physicists and engineers use notations such as \( \langle X \rangle \), \( \langle X \rangle_{\text{Av}} \), or X. In the cases mentioned, \( E(X) \) is given by Eqs. (2) and (3).

```
E(X) = $\sum$ p_i x_i

E(X) = $\int_{-\infty}^{+\infty}$ x F(x) dx
```

Before discussing the significance of the new concept, a few frequently used definitions are appropriate. Put \( m = E(X) \). Then \( X - m^2 \) is, of course, a random variable. In mechanics, its expectation represents the moment of inertia of the mass distribution. In probability, it is called the variance of X, given by Eq. (4). Its positive root is the standard deviation.

```
Var(X) = E((X - m)^2) = E(X^2) - m^2
```

The variance is a measure of spread: It is zero only if the entire mass is concentrated at the point \( m \), and it increases as the mass is moved away from \( m \). In the case of two variables \( X_1 \) and \( X_2 \) with expectations \( m_1 \) and \( m_2 \) it is necessary to consider not only the two variances \( s_1^2 = E[(X_1 - m_1)^2] \) but also the covariance \( Cov(X_1, X_2) = E[(X_1 - m_1)(X_2 - m_2)] = E[X_1X_2] - m_1m_2 \). The covariance divided by \( s_1s_2 \) is called the correlation coefficient of \( X_1 \) and \( X_2 \). If \( X_1 \) and \( X_2 \) are uncorrelated. Every pair of independent variables is uncorrelated, but the converse is not true.

# **Laws of large numbers.**

To explain the meaning of the expectation and, at the same time, to justify the intuitive frequency interpretation of probability, consider a gambler who at each trial may gain the amounts \( x_1, x_2, \dots \) with probabilities \( p_1, p_2, \dots \). The gains at the first and second trials are independent random variables \( X_1, X_2 \), with the indicated distribution and the common expectation \( m = \sum p_i x_i \). The event that an individual gain equals \( x_i \) as probability \( p_i \), and the frequency interpretation of probability leads one to expect that in a large number \( n \) of trials the event should happen approximately \( np_i \) times. If this is true, the total gain \( S_n = X_1 + X_2 + \dots + X_n \) should be approximately \( nm \); that is, the average gain \( (1/n)S_n \) should be close to \( m \). The law of large numbers in its simplest form asserts this to be true. See GAME THEORY; STATISTICS.



m. The law of large numbers in its simplest form asserts this to be true. See GAME THEORY; STATISTICS.

# **Proboisidice.**

An order of placental mammals derived from conservative (that is, primitive or ancient) hooved mammal stock (sometimes informally referred to as condylarths), the oldest members known from Pliocene sediments of North Africa.

At one point, probosideans had a wide distribution, having reached every continent except Australia and Antarctica. They included an astonishing variety of forms. Heretofore, currently the order consists of only two forms belonging to the family Elephantidae: the African elephant (Loxodonta africana) and the Asian elephant (Elephas maximus). Features commonly associated with the proboscideans include large body size, elongated snouts that form paired tusks (relatively small lower tusks were present in the jaws in the majority of extinct forms in addition), and a proboscis (often referred to informally as a trunk). It is important to realize that the very early forms lacked both significant tusks and a proboscis, yet these are still formally considered probosideans. Unlike modern mammals, which have reduced the tooth number to four or, in many cases, one, probosideans have retained five teeth. Throughout their known history, probosideans have been strictly herbivorous.

Early elephant evolution is known mainly from Africa during the Eocene and Oligocene. Near the beginning of the Miocene, probosideans existed in Africa and spread all over Europe and Asia, and by the middle Miocene they reached North America. The probosideans were highly successful in North America and, between 2 and 1.5 million years ago, they entered South America across the Panamanian landbridge. Between 12,000 and 10,000 years ago, most of the world’s probosideans became extinct, with only the African and Asian elephants surviving.

There has been considerable debate by paleontologists as to which animals are actually probosideans, in part because some members of the order bear little or no superficial resemblance to modern forms. Two suborders in the classification below, Deinotherioidea and Barytherioidea, represent two somewhat disputed groups.

+   Order Probosidea
+     Suborder Deinotherioidea
+       Family Deinotheriidae
+     Suborder Moeitherioida
+       Family Elephantidae
+     Infracorder Mammuthoidea
+       Family Mammuthidae
+     Infracorder Gomphotheroidea
+       Family Gomphotheridae
+       Family Elephantidae

The conservative probosideans consist of the members of the suborders Deinotherioidea, Barytherioidea, and Moeitherioidea. Though these animals are considered to be probosideans, they mostly bear little or no resemblance to elephants. In fact, the typically elephantine characters like tusks and a proboscis do not strictly define the order Probosidea. Instead, probosideans are characterized by relatively obscure features in the tooth, shoulder, and ankle. The relationship of these suborders to the advanced suborder Elephantoida (which includes the living elephants) is not well understood. See ELEPHANT; MAMMAL.

# **Procellariiformes.**

A large order of strictly marine birds found far offshore except when breeding. The procellariiforms, or tube-nosed swimmers, are most closely related to their descendant group, the penguins. The Procellariiformes comprise four families: Diomedeidae (albatrosses; 13 species); Procellariidae (shearwaters, petrels, and fulmars; 66 species); Hydrobatidae (storm petrels; 21 species); and Pelagodromidae (diving petrels; 4 species).