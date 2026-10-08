# Managing Performance and Memory

MKL_DYNAMIC being TRUE, provides for optimal choice of the number of threads in the following cases:

+   If the requested number of threads exceeds the number of physical cores (perhaps because of hyper-threading), and MKL_DYNAMIC is not changed from its default value of TRUE, Intel MKL will scale down the number of threads to the number of physical cores.

+   If you are able to detect the presence of MPI, but cannot determine if it has been called in a thread-safe mode (it is impossible to detect with MPICH 1.2.x, or MKL_DYNAMIC has not been changed from its default value of TRUE, MKL will run one thread.

# MKL_DOMAIN_NUM_THREADS

MKL_DOMAIN_NUM_THREADS accepts a string value <MKL-env-string>, which must have the following format:

```
<MKL-env-string> ::= <MKL-domain-env-string> { <delimiter>
MKL-domain-env-string> >
```

```
<delimiter> ::= <space-symbol>* { <space-symbol>
```

```
<MKL-domain-env-string> ::= <MKL-domain-env-name> <uses>
<number-of-threads>
```

```
<MKL-domain-env-name> ::= MKL_ALL | MKL_BLAS | MKL_FFT | MKL_VML
<uses> ::= [ <space-symbol> ] ( <space-symbol> ) <equality-sign> |
<comma-symbol> ] [ <space-symbol> ]
```

```
<number-of-threads> ::= <positive-number>
<positive-number> ::= <decimal-positive-number> | <octal-number> | <hexadecimal-number>
```

In the syntax above, MKL_BLAS indicates the BLAS function domain, MKL_FFT indicates non-cluster FFTs, and MKL_VML indicates the Vector Maths Library.

For example:

```
MKL_ALL 2 : MKL_BLAS 1 : MKL_FFT 4
MKL_ALL=2 : MKL_BLAS=1 : MKL_FFT=4
MKL_ALL,2, MKL_BLAS=1, MKL_FFT=4
MKL_ALL=2; MKL_BLAS=1; MKL_FFT=4
MKL_ALL = 2 MKL_BLAS 1 , MKL_FFT 4
MKL_ALL,2: MKL_BLAS 1, MKL_FFT, 4 .
```