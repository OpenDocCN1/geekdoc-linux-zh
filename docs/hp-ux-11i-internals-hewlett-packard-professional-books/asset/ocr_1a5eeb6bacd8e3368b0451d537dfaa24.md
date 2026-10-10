# CHAPTER 12

# Multiprocessing and HP-UX

There are many challenges in the implementation of a multiprocessor computer system. One of the first decisions to be made is whether the system will be symmetric or asymmetric. In a symmetric system, all processors have equal access to the system and play equal roles. In an asymmetric system, one processor is “in charge,” and it delegates work to the others.

With the exception of some boot time tasks, HP-UX is symmetric. During boot, one processor does the initial bring-up, but once the other processors are started, all have equal access. (See Chapter 15, “System Initialization,” for details of the system boot process). The HP-UX implementation has the following characteristics:

+   * Each processor has equal access to all system resources.
+   * System memory is shared by all processors.
+   * All I/O devices are shared by all processors.
+   * All processors execute a single copy of the kernel.

As with any design consideration, there are benefits to this design and there are design challenges. In this chapter, we look at how we take advantage of the benefits of multiprocessing and how we address some of the problems caused by having multiple processors.

# Hardware Overview

Figure 12-1 shows an example of a typical multiprocessor system.

![](bbox=[0.05, 0.86, 0.95, 0.99])