
## 2.3 Test Kernel: Polynomial Evaluation 53

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_58_0.png)

**FIGURE 2.1** S_overall versus time, optimized for S_optimized = 10 and 1000.

different optimization speed factors, S_optimized = 10 and S_optimized = 1000. As shown in the plot, the overall speed does not diverge significantly until time_optimized = 90%, and the relative difference between the curves is only a factor of 4.1 × when time_optimized = 97%! This basically means that the overall speed is 250 times less than that of our kernel speed when the kernel consumes 97% of the execution time.

## 2.3 TEST KERNEL: POLYNOMIAL EVALUATION

This section introduces a benchmark kernel that used throughput this chapter and Chapter 5 to describe and evaluate code optimizations. The kernel evaluates a degree-eight polynomial at every point in a vector x:

```
d(x) = \sum_{j=0} a_j x^j
```

Horner's method, an iterative method that evaluates the polynomial by repeatedly adding each and multiplying by x:

```
d_0(x) = a_7
d_1(x) = d_0(x)x + a_6
d_2(x) = d_1(x)x + a_5
d_3(x) = d_2(x)x + a_4
d_4(x) = d_3(x)x + a_3
d_5(x) = d_4(x)x + a_2
d_6(x) = d_5(x)x + a_1
d_7(x) = d_6(x)x + a_0
```

## 54 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Begin implementing Horner's method in C to determine how well the compiler optimizes it automatically. Set the input and output array size to be 128 MB.

```c
#define N 128*1024*1024
```

First, declare and initialize an array for the polynomial coefficients. Their values would not affect performance (assuming they do not cause floating-point exceptions). Assume the coefficients are ordered from highest order to the lowest:

```c
static float coeff[8] = {1.2,1,4.1,6,1.8,2.0,2.2,4.2,6};
```

Since N represents the size of the dataset in bytes, the array sizes must match the size of a float:

```c
static float x[N/4],d[N/4];
```

For this kernel it is useful to measure performance in terms of floating-point throughput, so augment the cnt_dump function from Chapter 1 to calculate floating-point operations per second, or flops. For a degree-8-polynomial, there are 14 floating-point operations per element.

Since the floating-point operations are the only operations that directly contribute to progressing the objective of the kernel, it may provide insight to measure code efficiency in terms of number of executed instructions per floating-point operation, which the instrumentation code can compute and print:

```c
float flops,mflops,ips;

flops = (float)N/4.0 * 14; // 14 ops per output value

mflops = flops/time/1.0e6;

ips = (float)(perf_count(cnts[INSTRUCTIONS])) / flops;
```

```c
printf("[perf_event] mflops%%0.2f, instructions per flop=\n%%0.2f\n",mflops, ips);
```

Change the memory bandwidth calculation to reflect that the code is now reading and writing the number of bytes specified by N:

```c
membw = (float)N*2.0/time/(1024.0*1024.0);
```

Next, populate the input array x with random numbers. Like the coefficient values, the input values are not important as long:

- 1. there is diversity in the values to improve the chance that logical errors in the code will cause a mismatch between two implementations,
- 2. the values do not cause floating-point exceptions:

```c
for (i=0;i<N/4;i++) x[i]=(float)rand()/(float)RAND_MAX;
```

Use the performance counter to instrument a naïve version of Horner’s method:

```c
float *d, *x, *d_test;
int i,j;
int fd[5];
unsigned long long cnts[4][3];
float coeff[32] = {1.2,1.4,1.6,1.8,2.0,2.2,2.4,2.6};

d=(float*)malloc(N);
x=(float*)malloc(N);
if (id || !x) err("malloc())");

for (i=0;i<N/4;i++) x[i]=(float)rand()/(float)RAND_MAX;

nts_tick(fd);
for (i=0;i<N/4;i++) (
	(the outer loop)
	d[i]=coeff[0];
	for (j=1;j<8;j++) (
		(the inner loop)
		d[i]=d[i]*x[i] + coeff[j];
	)
)

nts_tick(fd);
for (i=0;i<N/4;i++) (
	(the outer loop)
	d[i]=coeff[0];
	for (j=1;j<8;j++) (
		(the inner loop)
		d[i]=d[i]*x[i] + coeff[j];
	)
)
```

## 2.4 Using Multiple Cores: OpenMP

## CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

The ARM11 has one core. The ARM9 has two cores. The ARM15 has four cores. The Raspberry Pi has two cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four cores. The Raspberry Pi has four

## 2.4 Using Multiple Cores: OpenMP 57

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_62_0.png)

**FIGURE 2.2** OpenMP thread creation. per_event tracks performance events only within the master thread (solid line).

The most commonly used

The most commonly used OpenMP directive is the *parallel* directive, which specifies the start of a *parallel region*:

```c
#pragma parallel <directive options>
```

## 2.4.1 OpenMP directives

OpenMP includes a directive that allows
