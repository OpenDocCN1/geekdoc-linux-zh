
Maxima 5.42.1 `http://maxima.sourceforge.net`

Using Lisp Commonisp (GCL) 2.6.12

Distributed under the GNU Public License, see the file `COPYING`.

Dedicated to the memory of Wilhelm Scheter.

The function `help(report)` provides help information

```
(%1) eqn := diff(y, t, 2)+t*diff(y, t, 1)*t*y^2 = 0;

(%so1)      d dy 2

      t = -- + t --      dt

(%2) ode2(eqn, y, t);

(%3) y = bessel_y(0, t) %k2 + bessel_j(0, t) %k1

(%4) sol: bc2(0, {t=1, y=1, t=100}, $sol);
```
