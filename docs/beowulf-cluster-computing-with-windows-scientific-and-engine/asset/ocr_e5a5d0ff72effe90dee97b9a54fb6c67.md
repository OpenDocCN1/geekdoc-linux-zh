a system on a long-term throughput basis, as a contrast to conventional benchmark performance testing.

Clearly, no single type of performance measurement—much less a single figure of merit—is simultaneously easy to determine and completely informative. In one sense, only one figure of merit matters, as emphasized above: the wall clock run time for your particular application on your particular system. But this is not easy to determine before a purchase or upgrade decision has been made. And even if you can make such a measurement, it is not clear how to compare your results with the thousands of other Beowulf system users around the world, not to mention other types of systems and clusters.

These considerations have led many users of parallel and cluster systems to compare performance based on a few standard benchmark programs. In this way, you can determine whether your particular system design is as effective (as measured by a handful of benchmarks) as another. Such comparisons might not be entirely relevant to your particular application, but with some experience you can find one or more well-known benchmarks that give performance figures that are well correlated with your particular needs.

# ## 8.2  Ping-Pong Test

One of the most widely used measurements performed on cluster systems is the Ping-Pong test, one of several test programs that measure the latency and bandwidth of the interprocessor communications network. There are a number of tools for testing TCP performance, including **netperf** and **netpipe** (see **www.netperf.org** and **www.ameslab.gov/netpipe**). Ping-Pong tests that are appropriate for application developers measure the performance of the user API and are typically written in C and assume that the MPI communications library is installed on the system. More details on downloading and running these are given in Section 10.10.

# ## 8.3  The LINPACK Benchmark

The LINPACK benchmark dates back to the early 1980s, when Jack Dongarra (then at Argonne National Laboratory) began collecting performance results of systems, based on their speed in solving a 100 × 100 linear system using Fortran routines from the LINPACK library. While a problem of this size is no longer a supercomputer-class exercise, it is still useful for assessing the computational performance of a single-processor system. In particular, it is a reasonable way to