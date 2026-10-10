**6.2.3B** Show that the number of partitions of $n$ into exactly $k$ parts is at least $\lceil(1/k!\,C(n-1,k-1)\rceil$.

**6.2.4A** Let $u_k(n)$ be the number of ways that the integer $n$ can be expressed as a sum of *distinct positive integers of unequal size whose size is at most $k$*. Prove that, for all positive integers $k, n$ with $k<n$, we have $u_k(n)=u_{k-1}(n)+u_{k-1}(n-k)$.

**6.2.4B** Let $s_k(n)$ be the number of partitions of $n$ into distinct parts of which the smallest is of size $k$. Prove that, for all positive integers $k,n$ with $k<n$, we have $s_k(n)=s_{k+1}(n+1)+s_k(n-k)$. (*Hint: Split the partitions of $n$ according to whether they (i) do have or (ii) do not have just one part of size $k$. For partitions of type (i) form a partition of $n+1$ by adding one new dot to the smallest part.*)

**6.2.5A** Show, using Theorem 6.4(iii) that $p_k(n)$ is the integer nearest to $\frac{1}{12}(n+3)^2$.

**6.2.5B** Use Theorem 6.4(ii) to show that
i. For all positive integers $n$, $\frac{1}{12}n^2<p_k(n)$, and
ii. There is an integer $n_0$ such that for all integers $n\geq n_0$, $p_k(n)\leq\frac{1}{12}n^2$.

**6.2.6A** Show that, for all integers $n\geq 3$, $\lfloor\frac{1}{2}n+1\rfloor+\lceil\frac{1}{2}(n-3)+1\rceil=n$. (*Hint: Treat the cases where $n$ is even and $n$ is odd separately.*)

**6.2.6B** Show that, for all positive integers $m, \lfloor\frac{1}{4}m\rfloor+\lfloor\frac{1}{4}(m+1)\rfloor+\lfloor\frac{1}{4}(m+2)\rfloor=m$.

# **6.3 A BIT OF SPECULATION**

It follows from Theorem 6.4(ii) and (iii) that $p_2(n)\geq n/2=n/(1!2!)$ and $p_3(n)\geq n^2/12=n^2/(2!3!)$. This is scant basis for making a conjecture, but we shall be bold!

# Conjecture

For all positive integers $n,k$ with $k\leq n$, we have

$$p_k(n)\geq\frac{n^{k-1}}{(k-1)!(k!)}.$$

# Comment

It is a consequence of the logical order of presentation of mathematical arguments that the lemma must be presented before it can be used in the following theorem. However, let no one persuade you that some clever person thought up the lemma and then, hey presto!, found a theorem needing precisely that lemma. No! The main aim is to prove the conjecture, and the proof needs a bit of technical argument in the middle, which we have extracted as a lemma so that the proof of the theorem doesn’t get clogged up with technicalities.

# **Lemma 6.5**

Let $t$, $r$, and $n$ be real numbers such that $t\geq 2$, $r\geq 0$, and $(r+1)t\geq n$. Then,

$$ (n-rt)^{t-2} > \left[ \frac{(n-rt)^{t-1} - (n-(r+1)t)^{t-1}}{t(t-1)} \right], $$