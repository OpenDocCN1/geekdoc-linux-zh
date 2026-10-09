Apache Server 2.0 makes Apache a more flexible, more portable, and more scalable Web solution than ever before. The new 2.0 releases offer many improvements; the major improvements are discussed in the following sections.

# Multiprocessing modules

The first major change in Apache 2.0 is the introduction of multiprocession modules (MPMs). To understand why MPMs are created, you need to understand how Apache worked before. Apache Version 1.3 or earlier used a preforking architecture. In this architecture, an Apache parent process forked a set of child processes, which serviced the actual requests. The parent process simply monitored the children and spawned or killed child processes based on the amount of requests received. Unfortunately, this model didn't work well under platforms that are not process-centric such as Windows. So, the Apache Group came up with the MPM-based solution.

Each MPM is responsible for starting the server processes and for servicing requests via child processes or threads depending on the MPM implementation. Several MPMs are available. They are discussed in the following sections.

# The prefork MPM

The prefork MPM mimics the Apache 1.3 or earlier architecture, creating a pool of child processes to service requests. Each child process has a single thread. For example, if Apache starts 30 child processes, it can service 30 requests simultaneously.