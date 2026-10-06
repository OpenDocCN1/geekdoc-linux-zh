# # 13.3. Performance Tuning on Linux

Even with the holes just mentioned, Linux is still an ideal place to find and fix performance problems. It was written for developers by developers and, as a result, it is very friendly to the performance investigator. Linux has a few characteristics that make it a great platform to track down performance problems.

# ## 13.3.1. Available Source

First, a developer has access to most (if not all) source code for the entire system. This is invaluable when tracking down a problem that appears to be outside of your code. On a commercial UNIX or other operating systems where source is not available, you might have to wait for a vendor to investigate the problem, and you have no guarantee that he will fix it if it is his. However, on Linux, you can investigate the problem yourself and figure out why the performance is happening. If the problem is outside your code, you can fix it and submit a patch, or just run with a fixed version. By reading the source of the Linux code, you realize that the problem is in your code, you can then fix the problem. In either case, you can fix it immediately and are not gated by waiting for someone else.

# ## 13.3.2. Easy Access to Developers

The second advantage of Linux is that it is relatively easy to find and contact the developers of a particular application or library. In contrast to most proprietary operating systems, where it is difficult to figure out which engineer is responsible for a given piece of code, Linux is much more open. Usually, the names or contact information of the developers for a particular piece of software are with the software package. Access to the developers allows you to ask questions about how a particular piece of code behaves, what slow-running code intends to do, and whether a given optimization is safe to perform. The developers are usually more than happy to help with this.

# ## 13.3.3. Linux Is Still Young

The final reason that Linux is a great platform on which to optimize performance is because it is still young. Features are still being developed, and Linux has many opportunities to find and fix performance bugs. Because most developers focus on adding functionality, performance issues can be left unresolved. An ambitious performance investigator can find and fix many of the small performance problems in the ever-developing Linux. These small fixes go beyond a single individual and benefit the entire Linux community.