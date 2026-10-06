# 4.4 Step 3: Design a reproducible experiment

# 4.3 STEP 2: DETERMINE WHETHER THE BOTTLENECK CAN BE AVOIDED

At this point, we should understand the interaction between the code and the limiting resource, which manifests itself as the problem. Before moving further, verify that the problematic work is really necessary and unavoidable. This is especially important when dealing with large or old codebases, which are heavily modified from their original design and on systems that may violate order assumptions.

For instance, an old codebase for a disk I/O intensive application may have been heavily optimized to minimize the hard drive's spinning-plate times. This application might now be run on systems consisting of scheduling reads and writes wasteful. If the problem from Step 1 was caused by scheduling overhead, a solution would be to simply disable the seek-time optimizations when running on flash storage.

Another way to avoid performance issues is through the tunable parameters exposed via the software. Many applications provide configurability in buffer and cache sizes, timeouts, thresholds, and so on. A prime example of this is `sysctl` for the Linux kernel, exposed through `/proc/sys` and often configured at boot by `/etc/sysctl.conf`. This interface allows the user to change runtime parameters that affect the Linux kernel's behavior, and thus its performance.

If the work is deemed necessary, may still be possible to avoid a significant portion of it by utilizing caching. Expensive computations can be precomputed into a lookup table, trading memory usage for processing power. Computations that are computed frequently can also be cached via memoization, where the result of the computation is cached after its first evaluation.

For expensive calculations, also consider the precision required by the application. Sometimes it is possible to replace an expensive and precise calculation with a cheaper but less precise estimation.

# 4.4 STEP 3: DESIGN A REPRODUCIBLE EXPERIMENT

At this point, we should design an experiment to demonstrate the problem. The goal here is to isolate the problem in a way that it is easy to verify and share. A well designed experiment should follow the following criteria.

+   First, the experiment must clearly display the current performance numbers in an automated fashion. Whether the calculations or the actual experiment should require any human interaction. This will save time otherwise verifying that everyone is computing things properly. The performance numbers should be calculated exactly as described in the problem statement. Also, make sure to keep output formatting consistent and unambiguous. Aside from always labeling units, it may be helpful to mark which metrics are higher-is-better (HIB), lower-is-better (LIB), or nominal-is-better (NIB).