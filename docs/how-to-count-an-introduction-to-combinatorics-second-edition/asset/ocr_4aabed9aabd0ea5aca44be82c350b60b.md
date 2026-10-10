we see that the constant $\alpha$ has to satisfy the equation $\alpha = 2\alpha + 1$ and hence $\alpha = -1$. Thus the general solution of Equation 1 is $a_{n}=A(2^{n})-1$. Since $a_{1}=1, 2A-1=1$, and hence $A=1$. Therefore $a_{n}=2^{n}-1$. It follows that with 64 disks the process takes $2^{64}-1$ moves. You can check that $2^{64}-1$ seconds comes to about $5.8 \times 10^{9}$ years.

7.6.5A i. Suppose the recurrence relation $r_{n}-r_{n-1}=2n^{2}-3n+2$ has a solution of the form $r_{n}=En^{2}+Dn+C$, where $C, D$, and $E$ are constants. Substituting this into the recurrence relations gives that, for each positive integer $n$,

(En$^{2}+$Dn$+C$)-(E(n$-1)^{2}+$D(n$-1)+C)=2n^{2}-3n+2.

Therefore, for each positive integer $n$,

$2En+D-E=2n^{2}-3n+2.$

This is clearly impossible as a linear polynomial cannot be identically equal to a quadratic polynomial. This shows that the recurrence relation has no solution of the given form.

ii. If we substitute $r_{n}=En^{2}+Dn+C$ in the recurrence relation $r_{n}-2r_{n-1}=2n^{2}-3n+2$, we obtain

$(En^{2}+Dn+C)-2(E(n-1)^{2}+D(n-1)+C)=2n^{2}-3n+2.$

This gives

$-En^{2}+(4E-D)n+(-2E+2D-C)=2n^{2}-3n+2.$

Equating the coefficients of $n^{2}$ and $n$ and the constant terms gives $-E=2, 4E-D=-3$, and $-2E+2D-C=2$, giving $E=-2, D=-5$, and $C=-8$. It follows that $r_{n}=-2n^{2}-5n-8$ is a solution of the recurrence relation.

7.6.6A i. We prove the result by mathematical induction. We have $r_{2}-r_{1}=f(2)$. Hence $r_{2}=r_{1}+f(2)$, and so the result is true for $n=2$. Suppose that the result holds for $n=m$, so that $r_{m}=r_{1}+\sum_{k=2}^{m}f(k)$. Then, as $r_{m+1}-r_{m}=f(m+1)$, we have

$r_{m+1}=r_{m}+f(m+1)=r_{1}+\sum_{k=2}^{m}f(k)+f(m+1)=r_{1}+\sum_{k=2}^{m+1}f(k).$

Hence the result holds also for $n=m+1$. Therefore, by mathematical induction, it holds for all $n\geq 2$.

ii. It follows that the solution of Equation 7.49 is given by

$r_{n}=0+\sum_{k=2}^{n}2k^{2}-3k+2=n\left(\frac{n(n+1)(2n+1)}{6}-1\right)-3\left(\frac{n(n+1)}{2}-1\right)+2(n-1)$,