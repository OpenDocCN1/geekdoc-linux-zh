# 11 Intel® Math Kernel User's Guide

# Intel® Optimized MP LINPACK Benchmark for Clusters

The Intel® Optimized MP LINPACK Benchmark for Clusters is based on modifications and additions to HPL 2.0 from Innovative Computing Laboratories (ICL) at the University of Tennessee, Knoxville (UTK). The Intel Optimized MP LINPACK Benchmark for Clusters can be used for Top 500 runs (see http://www.top500.org). To use the benchmark you need to be familiar with the HPL distribution and usage. The Intel Optimized MP LINPACK Benchmark for Clusters provides some additional enhancements and bug fixes designed to make the HPL usage more convenient, as well as explain Intel® MPI settings that may enhance performance. The ./benchmarks/mp_linpack adds techniques to minimize search times frequently associated with long runs.

The Intel® Optimized MP LINPACK benchmark for Clusters is an implementation of the Massively Parallel MP LINPACK benchmark by means a random (Ax=b) system of linear equations measures the time it takes to factor and solve the system, converts that time into a performance rate, and tests the results for accuracy. You can solve any size (N) system of equations that fit into memory. The benchmark uses full pivoting to ensure the accuracy of the results.

Use the Intel Optimized MP LINPACK Benchmark for Clusters on a distributed memory machine on a shared memory machine use the Intel Optimized MP LINPACK Benchmark.

Intel provides optimized versions of the LINPACK benchmarks to help you obtain high LINPACK benchmark results on your systems based on genuine Intel® processors more easily than with the HPL benchmark. Use the Intel® Optimized MP LINPACK Benchmark to benchmark your cluster. The prebuilt binaries require that you first install Intel® MPI 3.x be installed on the cluster. The version of Intel MPI is free and can be downloaded from www.intel.com/software/products/cluster.

The Intel package includes software developed at the University of Tennessee, Knoxville, Innovative Computing Laboratories and neither the University nor ICL endorse or promote this product. Although HPL 2.0 is redistributable under certain conditions, particular package is subject to the Intel MKL license.

Intel MKL has introduced a new functionality to MP LINPACK which is called a hybrid build the term "hybrid" refers to special optimizations to take advantage of mixed OpenMP*/MPI parallelism. If you want to use one MPI process per node and achieve further parallelism by means of OpenMP use the hybrid build. In general, the hybrid build is useful when the number of MPI processes per core is less than one. If you want to rely exclusively on MPI for parallelism and use one MPI per core, use the non-hybrid build.

In addition to certain hybrid prebuilt binaries, Intel MKL supplies some hybrid prebuilt libraries to take advantage of the additional OpenMP* optimizations.