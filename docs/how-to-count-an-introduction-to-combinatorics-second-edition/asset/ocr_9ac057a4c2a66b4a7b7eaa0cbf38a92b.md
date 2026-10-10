since the infinite product converges for |z|<1. The coefficients in the power series $\sum_{n=0}^{\infty} a_n z^n$ for a complex function, *f*, are given by Cauchy’s formula

$a_n = \frac{1}{2\pi i}\oint_C \frac{f(z)}{z^{n+1}}dz$,

where *C* is a suitably chosen contour. Since *p*(*n*) is the coefficient of $z^n$ in the power series for the generating function *P*, it is given by

$p(n) = \frac{1}{2\pi i}\oint_C \frac{P(z)}{z^{n+1}}dz, \tag{8.33}$

where *C* is any simple closed contour that surrounds the origin and is wholly inside the unit disk, $D_1=\{z\in\mathbb{C}: |z|<1\}.$

It follows from this that the values of *p*(*n*) can be approximated by estimating the contour integral in Equation 8.33. This is, however, more easily said than done. The biggest contributions to the values of the integral arise from parts of the contour nearest to the singularities of the integrand. The function *P* has a singularity at each point $z\in\mathbb{C}$, where $z^k=1$ for some positive integer *k*. Thus *P* has singularities at all the complex roots of 1, and these are distributed densely on the boundary of the unit disk, $D_1$. Thus every point of $D_1$ is an essential singularity of *P*. This leads to tremendous technical difficulties.

In a celebrated paper published in 1918, G.H. Hardy and S. Ramanujan$^\ast$ overcame these difficulties and derived a remarkable formula that approximates *p*(*n*) very accurately. It is not possible to describe their method here. However, it is possible to give some idea of the formula that they derived.

The first two terms of their formula are

$\frac{1}{2\sqrt{2\pi}} \frac{d}{dn}\left( \frac{e^{(\pi/3)\sqrt{2n- (1/24)}n}}{\sqrt{n-(1/24)}} \right) + \frac{(-1)^n}{2\pi} \frac{d}{dn}\left( \frac{e^{(\pi/6)\sqrt{2n- (1/24)}n}}{\sqrt{n-(1/24)}} \right), \tag{8.34}$

Here *d/dn* denotes differentiation with respect to *n*. We use $HR_S(n)$ for the formula in expression 8.34. Hardy and Ramanujan were able to use the first term of their series to derive the following asymptotic formula for *p*(*n*):

$p(n) \sim \frac{1}{4\sqrt{3n}} e^{\pi\sqrt{2n/3}}, \tag{8.35}$

$^\ast$ G.H. Hardy and S. Ramanujan, *Asymptotic Formulae in Combinatory Analysis, Proceedings of the London Mathematical Society*, (2), 17 (1918), pp 75–115.