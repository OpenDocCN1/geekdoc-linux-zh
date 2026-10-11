
## 5. After you have determined a possible cause of the bottleneck and have fixed/tuned it, perform another user ramp-up test.
## 6. Repeat this process until you can max out the application server's CPU.

In the case of a clustered configuration, investigate the CPU utilization of all application server boxes. Test a clustered configuration only after you have done a single-server test. A clustered configuration is good for testing scalability problems. Also, it is recommended that you assign a box exclusively to an application server and move all other servers (database server, JMS server, and so on) to remote boxes. A later chapter illustrates this approach by using a real-life example.

When you have determined that a bottleneck exists, the next step is to look for it. It takes experience and exposure to a number of problem cases to be able to hunt down the culprit quickly. Some guidelines that we can offer include the following:

- Enterprise application. Make sure that the enterprise application is not causing the problem. Profile the application using tools to detect problems with path length, method time, memory usage, and thread waits. Some commercial tools for J2EE performance profiling that are now available on the Linux platform are JProbe from Quest Software, OptimizIt from Borland, and Rational Purify/Quantify from IBM. Eclipse is an open-source profiler available on Linux.

To be an expert performance analyst, you have to be familiar with J2EE programming concepts and the best programming practices for good performance.

- Java Virtual Machine. The JVM is crucial for the application server. Make sure that it is properly tuned based on the behavior of the enterprise applications. More specifically, check if the heap size is set properly. Examine the behavior of the garbage collector. Does using the parallel garbage collector help? If the JVM is based on hot-spot technology, is it enabled? Is large page support available, and does your Linux kernel support it as well? Is JIT enabled? These are just some of the things you can check.

The best thing you can do is check the JVM implementor's help guide or web site to find what parameters are available for tuning. If you intend to be an expert performance analyst for application servers, you must understand intimately the underpinnings of the Java Virtual Machine and some of its implementation details.

- Security. If the web server uses security, verify that it is tuned properly to handle SSL requests. Also, the application server might have some performance tuning knobs that are available for SSL or J2EE security. Security itself is an overhead. It is estimated that security can slow down an application server by 20% to 25%. Test your system by turning off security, and check if you are getting a lot more than this percentage.

- Networking. Because the application server is very intensive with network communications to the web server, database server, JMS server, LDAP server, and other remote servers, verify that the TCP/IP stack is properly tuned. It is also important to check the performance of the servers that the application server is talking to. For example, check if the database server is properly tuned and if it can process the amount of data being passed to it by the application server in a timely manner. Another critical server to look at is the web server. In these situations, you might need the help of other people with the necessary skills to examine those servers.

- File system. Take note of the file system activity by using tools such as sar and iostat. Also check to see if a lot of file swapping is occurring.

- Concurrency. If you are using kernel 2.4, examine the context switches that are taking place by running vmstat. If the context switches are a bit too high, make sure that the application server's thread pool is not too high. Typically, a thread pool of 10 to 20 threads is sufficient. Beyond that, performance can degrade. With NPTL supported in the Linux 2.6 kernel, this limitation might be alleviated.

- Memory. Check the system memory usage specifically, the memory that is allocated to the application server. Determine if the system needs to be upgraded with more memory.

- Scaling. Verify that the system is scaling well. In SMP systems, if the number of processors is a detriment rather than a help, it might be wise to disable some of the processors. If vertical clustering is configured, make sure that there are not too many instances of the application server. Determine whether adding more application servers increases CPU utilization. If it does, kill some of your application servers.

Depending on the type of environment you have (for example, hyperthreading or NUMA), there might be other things you can look into. Verify that your Linux kernel supports these additional features on your system.

Tuning an application server is a system-wide activity. All the pieces of the system need to have a performance story, and you should be able to work on all the layers in the software performance stack. The application server is a complex piece of middleware and so is the tuning process.

## Summary

Application servers are complex pieces of middleware that have become some of the most useful tools in the IT industry today. Application servers are typically used by business enterprises to put their business on the Internet. The specific type of application server discussed in this chapter is the J2EE-based application server, which is currently the most widely used type of application server.

Characterizing the performance of an application server is not straightforward because doing so involves many external components. Those components need to be considered because their own performance affects the overall performance of the application server. We provided a software performance stack to illustrate the different layers of software that contribute to the performance of the application server. Each of these layers must be addressed individually to diagnose performance problems and improve performance.

We also provided some key concepts pertaining to the different ways of improving performance and high availability. The important thing to remember is that you have to determine the performance requirements of your enterprise—the anticipated volume of requests and the expected response time. From there, you can determine what the capacity of the system should be to meet those requirements. There are many topologies to choose from, but your decision depends largely on your requirements.

## References

- [1] Brown, K., G. Craig, G. Hester, et. al. *Enterprise Java Programming with IBM WebSphere*, 2nd Edition. Addison-Wesley, 2003.
- [2] Jones, S., R. Willenborg, and K. Hygh. *Performance Analysis for Java Web Sites*. Addison-Wesley, 2003. ISBN 0-20-184454-0.
- [3] Menasce, D. A. and V. A. F. Almeida. *Capacity Planning for Web Performance: Metrics, Models, & Methods*. Prentice Hall PTR, Upper Saddle River, New Jersey, 1998. ISBN 0-13-693822-1.

## Part V: Tuning Case Studies

- Chapter NINETEEN. Case Study: Tuning the I/O Schedulers in Linux 2.6
- Chapter TWENTY. Case Study: File System Tuning
- Chapter TWENTY-ONE. Case Study: Network Performance on Linux
- Chapter TWENTY-TWO. Case Study: Commercial Workload Tuning
- Appendix A. Tuning Kernel Parameters

# Chapter NINETEEN. Case Study: Tuning the I/O Schedulers in Linux 2.6

By Dominique Heger and Steven Pratt

## Introduction

The goal of this chapter is to quantify I/O performance in Linux 2.6 under varying workload conditions. These workload conditions are in environments ranging from single-CPU, single-disk setups to SMP systems that utilize large, sophisticated RAID systems. Incorporating different I/O workload patterns, the focus is on quantifying the baseline, as well as the optimized performance behavior under different Linux 2.6 I/O scheduler and file system configurations. The analysis results in the establishment of performance metrics that outline the I/O performance behavior and guide the configuration, setup, and fine-tuning process.

The point of convergence in the analysis is the entire I/O stack, incorporating the major software and hardware I/O optimization features that are present in the I/O path. The I/O stack in general has become considerably more complex over the last few years. Contemporary I/O solutions include hardware, firmware, and software support for features such as request coalescing, adaptive prefetching, automated invocation of direct I/O, or asynchronous write-behind policies. From a hardware perspective, incorporating large cache subsystems on a memory, RAID controller, and physical disk layer allows for a very aggressive utilization of these I/O optimization techniques. The interaction of the different optimization methods that are incorporated in the different layers of the I/O stack is neither well understood nor quantified to an extent necessary to make a rational statement on I/O performance. A rather interesting feature of the Linux operating system is the I/O scheduler. Unlike the CPU scheduler, an I/O scheduler is not a necessary component of any operating system per se. Therefore, it is not an actual building block in some of the commercial UNIX systems.

Before looking at the Linux 2.6 I/O schedulers and their performance, we first discuss the benchmark environment and workload profiles used throughout this chapter.
