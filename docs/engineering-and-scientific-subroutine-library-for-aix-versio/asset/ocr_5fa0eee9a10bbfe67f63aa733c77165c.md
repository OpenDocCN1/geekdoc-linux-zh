# **SSPR2, DSPR2, CHPR2, ZHPR2, SSYR2, DSYR2, CHER2, ZHER2, SSLR2, and DSLR2**

$n$  is the number of elements in vectors **x** and **y** and the order of matrix **A**.  
Specified as: a fullword integer; $n \geq 0$.

$alpha$  is the scaling constant $\alpha$.  
Specified as: a number of the data type indicated in Table 70 on page 319.

$x$  is the vector **x** of length $n$.  
Specified as: a one-dimensional array of (at least) length $1+(n-1)\lvert incx\rvert$, containing numbers of the data type indicated in Table 70 on page 319.

$incx$  is the stride for vector **x**.  
Specified as: a fullword integer, where:  
For SSPR2, DSPR2, CHPR2, ZHPR2, SSYR2, DSYR2, CHER2, and ZHER2, $incx < 0$ or $incx > 0$.  
For SSLR2 and DSLR2, $incx$ can have any value.

$y$  is the vector **y** of length $n$.  
Specified as: a one-dimensional array of (at least) length $1+(n-1)\lvert incy\rvert$, containing numbers of the data type indicated in Table 70 on page 319.

$incy$  is the stride for vector **y**.  
Specified as: a fullword integer, where:  
For SSPR2, DSPR2, CHPR2, ZHPR2, SSYR2, DSYR2, CHER2, and ZHER2, $incy < 0$ or $incy > 0$.  
For SSLR2 and DSLR2, $incy$ can have any value.

$ap$  has the following meaning:  
For SSPR2 and DSPR2, $ap$ is the real symmetric matrix **A** of order $n$, stored in upper- or lower-packed storage mode.  
For CHPR2 and ZHPR2, $ap$ is the complex Hermitian matrix **A** of order $n$, stored in upper- or lower-packed storage mode.  
For SSLR2 and DSLR2, $ap$ is the real symmetric matrix **A** of order $n$, stored in lower-packed storage mode.  
Specified as: a one-dimensional array of (at least) length $n(n+1)/2$, containing numbers of the data type indicated in Table 70 on page 319.

$a$  has the following meaning:  
For SSYR2 and DSYR2, $a$ is the real symmetric matrix **A** of order $n$, stored in upper or lower storage mode.  
For CHER2 and ZHER2, $a$ is the complex Hermitian matrix **A** of order $n$, stored in upper or lower storage mode.  
Specified as: an $lda$ by (at least) $n$ array, containing numbers of the data type indicated in Table 70 on page 319.

$Lda$  is the leading dimension of the array specified for $a$.  
Specified as: a fullword integer; $Lda > 0$ and $Lda \geq n$.

**On Return:**