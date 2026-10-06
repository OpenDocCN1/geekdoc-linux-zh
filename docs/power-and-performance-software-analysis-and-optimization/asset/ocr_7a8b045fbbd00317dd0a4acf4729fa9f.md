# CHAPTER
15
Exploiting Parallelism

+   CHAPTER CONTENTS
15.1 SIMD ................................................................................................................... 265
  15.1.1 SIMD Registers ........................................................................................................ 266
    Data Alignment............................................................................................................................... 267
    Handling Unknown Alignment............................................................................................... 268
  15.1.2 SIMD Operations ................................................................................................ 269
References ........................................................................................................................ 273

Parallelism, the act of performing two or more operations simultaneously, is a topic that has generated lots of interest and headlines within the last decade. Part of this fascination stems from the simplification of the consumer market away from uniprocessor (UP) systems to widely available symmetric multiprocessing systems (SMP). Another part of this interest stems from the simplification of GPGPU, that writing general purpose code for the GPU, which is a dedicated processor. This simplification has transformed highly parallel vector processing into a niche aspect of high performance computing (HPC) segment into something very accessible to everyone. Regardless of the modern attention, research into parallelism, and its associated challenges, traces back to the 1950s, predating the x86 architecture by more than twenty years.

Unfortunately, one hazard of the modern hype is the misconception that parallelism makes everything fast, or that each task yields well to parallelization. On the contrary, many tasks can't be parallelized in a manner that improves performance, and often parallel code will run slower than serial code. It is important to keep in mind that all of the other aspects introduced within this book, properly wielding parallelism requires measurement and careful analysis in order to determine whether it is an appropriate solution for a given problem.

The most discussed levels of parallelism utilize multiple threads and multiple processes. The decision between these two techniques revolves around whether the address space should be shared or isolated between the two components. In Linux, both threads and processes are created with the clone(2) system call, and processes can also be created with the fork(2) system call.