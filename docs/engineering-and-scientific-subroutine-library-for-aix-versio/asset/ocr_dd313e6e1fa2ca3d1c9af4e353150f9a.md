```
SUBROUTINE FUN1 (T,Y,N)
INTEGER*4 N
REAL*4 T(*),Y(*),TEMP
DO 1 I=1,N
 1          TEMP=1.0/T(I)
             Y(I)=EXP(TEMP)*TEMP**2
  RETURN
  END
```

**Program Statements and Input:**

  EXTERNAL FUN1

  .
  .
  .

```
                 SUBF      A      B      N
                 |         |      |      |
  XINT  = SGRAQ( FUN1 , -2.0 , 0.0 , 10 )
```

  .
  .
  .
  FUN1      = (see above)

**Output:**

  XINT    = 0.393

# **Example 2**

This example shows how to compute the integral of the function $f$ given by:

 $f(x) = (x - 3.0)^{-2} + 10(x - 3.0)^{-11}$

over the interval $(4.0, \infty)$, using the Gauss-Rational method with 6 points:

$$ \int_{4.0}^{\infty} \left( (x - 3.0)^{-2} + 10(x - 3.0)^{-11} \right) dx $$

The user-supplied subroutine FUN2, which evaluates the integrand function, is coded in Fortran as follows:

```
SUBROUTINE FUN2 (T,Y,N)
INTEGER*4 N
REAL*4 T(*),Y(*),TEMP
DO 1 I=1,N
 1          TEMP=1.0/(T(I)-3.0)
             Y(I)=TEMP**2+10.*TEMP**11
  RETURN
  END
```

**Program Statements and Input:**

  EXTERNAL FUN2

  .
  .
  .

```
                 SUBF      A      B      N
                 |         |      |      |
  XINT  = SGRAQ( FUN2 , 4.0 , -3.0 , 6 )
```

  .
  .
  .
  FUN2      = (see above)

**Output:**