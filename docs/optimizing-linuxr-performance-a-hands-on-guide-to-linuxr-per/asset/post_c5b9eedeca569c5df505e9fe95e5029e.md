
## 12.9. Testing the Solution

Because we have not solved the problem in the prelink code, but instead reported a bug, we cannot test the fixed prelink time against our original baseline immediately. However, if the author or maintainer is able to implement the proposed changes, or find a better way to optimize things, we will be able to check out the performance of the updated version when it arrives.

## 12.10. Chapter Summary

In this chapter, we started with a misbehaving system and used performance tools to pinpoint which subsystem was used excessively (the disk subsystem was shown by `vmstat`) and which component caused the problem (prelink). We then investigated the prelink application to determine why it used so much I/O (using strace). We discovered in prelink's cached mode that it should dramatically reduce disk I/O. We investigated the performance of the cached mode and found that it did not eliminate disk I/O as much as it did, because it was trying to prelink files that could not be prelinked. We then simulated a cache that avoided trying to prelink files that could not be prelinked and verified that it significantly reduced the amount of disk I/O and runtime of prelink in quick mode. Finally, we submitted a bug report to the author of prelink in the hopes that the author will recognize the problem and fix it. This chapter was the last chapter of Linux performance hunts.

In the next chapter, the final chapter, we look at the higher-level picture of Linux performance and performance tools. We review documentation methodologies and tools covered in this book and look at some of the areas of Linux performance tools that are ripe for improvement.

## Chapter 13. Performance Tools: What's Next?

This chapter contains musings about the current state of Linux performance tools, what still needs to be improved, and why Linux is currently a great platform to do performance investigation.

After reading this chapter, you should be able to:

- Understand the holes in the Linux performance toolbox, and understand some of the ideal solutions
- Understand the benefits of Linux as a platform for performance investigation

## 13.1. The State of Linux Tools

This book tours the current Linux performance tools, how to use them individually, and how to use them together to solve performance problems. As with every aspect of Linux, these performance tools are constantly evolving, so when investigating a problem, it is always a good idea to review the man page or documentation of a performance tool to determine whether its usage has changed. The fundamental functions of the performance tools rarely change, but new features are commonly added, so it is helpful to review the latest release notes and documentation for a given tool.

## 13.2. What Tools Does Linux Still Need?

As we toured the Linux tools, we saw some holes in the overall performance-investigation functionality. These holes are the result of kernel limitations, and some just exist because no one has written a tool to solve the problem. However, filling of these holes would make it dramatically easier to track down and fix Linux problems.

### 13.2.1. Hole 1: Performance Statistics Are Scattered

One glaring hole is that Linux has no tool that provides relevant performance statistics for a particular process. `ps` was to fill this hole in the original UNIX, and on Linux, it is pretty good but it does not cover all statistics that other commercial implementations provide. Some statistics are invaluable in tracking performance problems—for example, `inblk` (I/O blocks read in) and `outbl` (I/O blocks out) which indicate the amount of disk I/O is using; `vcsw` (voluntary context switches) and `incsww` (involuntary context switches), which often show the amount of network I/O an application is using.

### 13.2.2. Hole 2: No Reliable Call Tree

The next problem is that Linux lacks a tool that provides a complete call tree for a process. While tools like `perf` and `system` provide some information, they are often difficult to use or do not provide the full picture of the execution flow.

### 13.2.3. Hole 3: I/O Attribution

The final hole is the lack of a tool to accurately attribute I/O operations to specific processes or threads. This makes it difficult to identify the root cause of I/O related bottlenecks.

## 13.3. Performance Tuning on Linux

Even with the holes mentioned, Linux is still an ideal place to optimize performance. It was written for developers and, as a result, it is very friendly to the performance investigator. Linux has a few characteristics that make it great:

### 13.3.1. Available Source

First, a developer has access to most (if not all) source code for the entire system. This is invaluable when tracking down a problem that appears to be outside your code. On a commercial UNIX or other operating systems where source is not available, you might have to wait for a vendor to investigate the problem, and you have no guarantee they will fix it. However, on Linux, you can investigate the problem yourself and figure out why the performance is happening. If the problem is outside your code, you can fix it and submit a patch, or just run with a fixed version. By reading the source of the Linux code, you realize that the problem is in your code, you can then fix it. In either case, you can fix it immediately and are not gated by waiting for someone else.

### 13.3.2. Easy Access to Developers

The second advantage of Linux is that it is relatively easy to find and contact the developers of a particular application or library. In contrast to most proprietary operating systems, where it is difficult to figure out which engineer is responsible for a given piece of code, Linux is much more open. Usually, the names or contact information of the developers for a particular piece of software are with the software package. Access to the developers allows you to ask questions about how a particular piece of code behaves, what slow-running code intends to do, and whether a given optimization is safe to perform. The developers are usually more than happy to help with this.
