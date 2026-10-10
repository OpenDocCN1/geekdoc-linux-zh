
## Exercises

**4.3.1A** Use the formula in Equation 4.7 to calculate the values of $S(4,2)$ and $S(8,4)$, and check that the values you get agree with those given in Table 3.2.

**4.3.1B** Use the formula in Equation 4.7 to calculate the values of $S(7,k)$ for $1 \le k \le 7$, and check that the values you get agree with those given in Table 3.2.

**4.3.2A** Use the recurrence relation $S(n,k) = S(n-1,k-1) + kS(n-1,k)$ of Theorem 3.4, and the fact that $S(n,1) = 1$ for each positive integer, to give a proof of Theorem 4.5 by mathematical induction.

(Use induction on $n$ to prove that for every positive integer $n \ge 1$, for integers $k$ with $1 \le k \le n$, the formula in Equation 4.7 of Theorem 4.5 holds. This is a good example of a case where *once you know which formula it is you want to prove*, proof by mathematical induction is a useful tool. As you will see, it enables us to prove Equation 4.7 just by algebraic manipulations. However, it wouldn't be much use if all we had was the recurrence relation, and we didn't have any idea what the correct formula was.)

**4.3.2B** Verify that Theorem 4.5 gives the same answers as does Theorem 3.5 of Chapter 3; namely, that for all positive integers $n$, $S(n,1) = S(n,n) = 1$, and for $n \ge 2$, $S(n,2) = 2^{n-1} - 1$.

## CHAPTER 5
# Stirling and Catalan Numbers

### 5.1 STIRLING NUMBERS

One of the pleasures of studying mathematics lies in discovering how the same ideas, numbers, and so on keep cropping up in different settings. In the case of (collections of) numbers, in particular, many are named after famous mathematicians, often their originators or principal investigators. Apart from the well-known Fibonacci numbers, there are numbers named after Fermat, Bernoulli, Euler, Mersenne, Lucas, Carmichael, Ramsey (whom we meet in Chapter 16), and many more.*

In this chapter we consider just two classes of numbers, one named after the Scottish mathematician Stirling, the other after the French/Belgian mathematician Catalan. The former class was, indeed, introduced by Stirling, while the latter class was essentially introduced by Euler, with other mathematicians studying them before Catalan’s time. So, what problems gave rise to these numbers?

In his book *Methodus Differentialis* (1730; following a paper of the same name in 1719) James Stirling† introduced methods by which he could quickly determine, accurate to many decimal places, the approximate value of various slowly converging series. For example, he was able to calculate $\sum_{n=1}^{\infty}(1/n^2)$ to 17 places of decimals. (Proceeding naively would require, approximately, adding the first 1,000,000,000 terms!) To do this Stirling needed to determine the coefficients $a_{n,k}$ arising when the so-called *falling factorial polynomial* $x(x-1)(x-2)\cdots(x-[n-1])$ is written in the form $a_{n,n}x^n - a_{n,n-1}x^{n-1}+\cdots+(-1)^{n-1}a_{n,1}x$ (the minus signs being chosen so that all the terms $a_{n,k}$ are positive) as well as the converse problem of finding the coefficients $b_{n,k}$ arising when $x^n$ is expressed in terms of the falling factorial polynomials, so that

$$ x^{n}=b_{n,n} x(x-1)\cdots (x-[n-1])+b_{n,n-1} x(x-1) \cdots (x-[n-2])+... +b_{n,2} x(x-1)+b_{n,1} x. $$

> * Not forgetting Erdős! Paul Erdős, who was born in Budapest on March 26, 1913, was a prolific and towering figure in combinatorics. He wrote 1475 research papers, mostly in collaboration. Altogether he had some 485 coauthors. He died in Warsaw on September 20, 1996. Your Erdős number, if it exists, is the least integer $n$ such that there is a sequence of people $E_0, E_1, \ldots, E_n$, where $E_0$ is Erdős, $E_n$ is you, and for each $k, 0 \leq k < n, E_k$ has coauthored a published research paper with $E_{k+1}$. There is an excellent biography of Erdős, *The Man Who Loved Only Numbers*, by Paul Hoffman, Fourth Estate, London, 1998.

> † James Stirling was born in Scotland in 1692. He was a student in Glasgow and Oxford, and then went to Venice. He settled in London in 1724. In his later life Stirling turned his attention to engineering. He was employed by the Scottish Mining Company and moved back to Scotland in 1735 to Leadhills, Lanarkshire, a village near the company’s lead mines. He died in Edinburgh on December 5, 1770.

The definition of falling factorial polynomials given above is fairly easy to grasp, but clearly a succinct notation would be a help. So for each integer $k>0$ we use $[x]_k$ for the falling factorial polynomial $x(x-1)\cdots (x-[k-1])$. Note that the suffix $k$ indicates the degree of the polynomial.

#### PROBLEM 5.1

Calculate the values of the numbers $a_{n,k}$ for $1 \leq n \leq 5$ and $1 \leq k \leq n$.

**Solution**

- $[x]_1 = x$
- $[x]_2 = x(x-1) = x^{2}-x$
- $[x]_3 = x(x-1)(x-2) = x^{3}-3x^{2} + 2x$
- $[x]_4 = x(x-1)(x-2)(x-3) = x^{4}-6x^{3} + 11x^{2}-6x$
- $[x]_5 = x(x-1)(x-2)(x-3)(x-4) = x^{5}-10x^{4} + 35x^{3}-50x^{2} + 24x$

Therefore we have Table 5.1 giving the numbers $a_{n,k}$ for $1 \leq n \leq 5$ and $1 \leq k \leq n$.

#### PROBLEM 5.2

Calculate the numbers $b_{n,k}$, for $1 \leq n \leq 4$ and $1 \leq k \leq n$.

**Solution**

- $[x]_1 = x$, and hence $b_{1,1} = 1$.
- $[x]_2 = x^{2}-x$, and hence $x^{2}=[x]_2 + x = [x]_2 + [x]_1$, Therefore $b_{2,2} = 1$ and $b_{2,1} = 1$.
- $[x]_3 = x^{3}-3x^{2} + 2x$, and hence $x^{3}=[x]_3 + 3x^{2}-2x = [x]_3 + 3([x]_2 + [x]_1)-2[x]_1 = [x]_3 + 3[x]_2 + [x]_1$. Therefore $b_{3,3} = 1, b_{3,2} = 3$, and $b_{3,1} = 1$.
- $[x]_4 = x^{4}-6x^{3} + 11x^{2}-6x$, and hence $x^{4}=[x]_4 + 6x^{3}-11x^{2} + 6x = [x]_4 + 6([x]_3 + 3[x]_2 + [x]_1)-11([x]_2 + [x]_1) + 6[x]_1 = [x]_4 + 6[x]_3 + 7[x]_2 + [x]_1$. Therefore $b_{4,4} = 1, b_{4,3} = 6, b_{4,2} = 7$, and $b_{4,1} = 1$.

**TABLE 5.1**

| $a_{n,k}$ | $k=1$ | $k=2$ | $k=3$ | $k=4$ | $k=5$ |
| :--- | :---: | :---: | :---: | :---: | :---: |
| $n=1$ | 1 | | | | |
| $n=2$ | 1 | 1 | | | |
| $n=3$ | 2 | 3 | 1 | | |
| $n=4$ | 6 | 11 | 6 | 1 | |
| $n=5$ | 24 | 50 | 35 | 10 | 1 |

**TABLE 5.2**

| $b_{n,k}$ | $k=1$ | $k=2$ | $k=3$ | $k=4$ | $k=5$ |
| :--- | :---: | :---: | :---: | :---: | :---: |
| $n=1$ | 1 | | | | |
| $n=2$ | 1 | 1 | | | |
| $n=3$ | 1 | 3 | 1 | | |
| $n=4$ | 1 | 7 | 6 | 1 | |
| $n=5$ | 1 | 15 | 25 | 10 | 1 |

Using the same method you should find that $x^5 = [x_5] + 10[x_4] + 25[x_3] + 15[x_2] + [x_1]$.
Hence we have Table 5.2.

The above coefficients cry out for investigation. Do any of them ring any bells? Table 5.1 may not be familiar, but look at the entries in Table 5.2. Yes, they are the same as the numbers in Table 3.2 giving the values of $S(n,k)$. Recall that $S(n,k)$ is the number of ways of placing $n$ distinct balls in $k$ identical boxes, so that no box is empty. Comparing the two tables we see that for $1 \le n \le 5$ and $1 \le k \le n, b_{n,k} = S(n,k)$. Is this just a coincidence? As we now show, we can prove, using mathematical induction, that this equality is always true.

#### THEOREM 5.1

For each integer $n \ge 1$, we have

$$ x^n = S(n,n)[x_n] + S(n,n-1)[x_{n-1}] + \ldots + S(n,1)[x_1], $$

that is,

$$ x^n = \sum_{k=1}^{n} S(n,k)[x_k]. $$

**Proof**

*Base. As $S(1,1) = 1$, and $[x] = x$, we have that $x = S(1,1)[x_1]$, and so the result holds for $n = 1$.*

*Induction step. Suppose the result holds for $n = t$, that is, that*

$$ x^t = \sum_{k=1}^{t} S(t,k)[x_k]. \qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.1) $$

It follows from Equation 5.1 that

$$ x^{t+1} = x(x^t) = x \sum_{k=1}^{t} S(t,k)[x_k] = \sum_{k=1}^{t} S(t,k) x [x_k] = \sum_{k=1}^{t} S(t,k)[x_k][(x - k) + k]. \qquad\qquad\qquad\qquad (5.2) $$

Now $[x]_k (x-k)=x(x-1)(x-2)\cdots(x-[k-1])(x-k)=[x]_{k+1}$, and hence it follows from Equation 5.2 that

$$ x^{t+1}=\sum_{k=1}^{t} S(t, k)[x]_{k+1}+\sum_{k=1}^{t} k S(t, k)[x]_{k} $$
$$ \quad=S(t, 1)[x]_{1}+\sum_{k=2}^{t}\left(k S(t, k)+S(t, k-1)\right)[x]_{k}+S(t, t)[x]_{t+1} $$

Now, $S(t, 1)=1=S(t+1, 1), S(t, t)=1=S(t+1, t+1)$, and, by Theorem 3.4, $k S(t, k)+S(t, k-1)=S(t+1, k)$. Hence, it follows from Equation 5.3 that $x^{t+1}=\sum_{k=1}^{t+1} S(t+1, k)[x]_{k}$. Therefore the results hold also for $n=t+1$. It follows, by mathematical induction, that the result is true for all integers $n \geq 1$.

Problem 5.A is another instance where the numbers $s(n, k)$ arise. In calculus the operator $\Theta=x D=x(d x / d x)$ occurs frequently. We let, as usual, $\Theta^{0}$ and $D^{0}$ be these operators repeated $n$ times, so that, in particular, $D^{n}$ is the operator $d^{n} / d x^{n}$. Then, if $f$ is a function it can be differentiated as $O f$ as required, and $\theta f=x d f$. We see that $\theta^{2} f=\theta(x D f)=x D(x f+x^{2} D^{2} f)=x D f+x^{2} D^{2} f$. (Note that $D(x D f)=D f+x^{2} D f$ is obtained by applying the product rule to differentiate the product $x d f$.) Thus the operators $\theta: x D$ and $x D+x^{2} D^{2}$ are identical.

#### PROBLEM 5.3

Show that $\Theta^{3}=x D+3 x^{2} D^{2}+x^{3} D^{3}$, and find a similar expression for $\Theta^{4}$.

**Solution**

We have that $\Theta^{3}=\Theta(\Theta^{2})=x D(x D+x^{2} D^{2})=x[D+x D]+\left[2 x^{2} D^{2}+x^{3} D^{3}\right]=x D+3 x^{2} D^{2}+x^{3} D^{3}$.
Similarly, $\Theta^{4}=\Theta(\Theta^{3})=x D(x D+3 x^{2} D^{2}+x^{3} D^{3})=x[D+x D]+\left[6 x^{2} D^{2}+3 x^{3} D^{3}\right]+\left[3 x^{2} D^{3}+x^{3} D^{3}\right]=x D+7 x^{2} D^{2}+6 x^{3} D^{3}+x^{4} D^{4}$.

At this stage, you will notice that the coefficients $1,7,6,1$ that occur in this last expression are the values of the Stirling numbers, $S(4, k)$, for $k=1,2,3,4$. We ask you to prove that this generalizes in Exercise 5.1.7.B.

The numbers $S(n, k)$ are usually called *Stirling numbers of the second kind*. The numbers $a_{n, k}$ were also introduced by Stirling and are usually called *Stirling numbers of the first kind*. We shall use the notation $s(n, k)$ for these numbers. As the names “Stirling numbers of the second kind” and “Stirling numbers of the first kind” are rather cumbersome, we shall follow the notation $S(n, k)$ and $s(n, k)$ and call these numbers *Stirling numbers* and *stirling numbers*, respectively.

Therefore, we define the *stirling number*, $s(n, k)$, as follows.

#### DEFINITION 5.1

For each pair of integers $k, n$ such that $1 \leq k \leq n$ we define the *stirling number*, $s(n, k)$, to be the modulus of the coefficient of $x^{k}$ in the expansion of $[x]_{n}$. That is, $s(n, k)=a_{n, k}$.
