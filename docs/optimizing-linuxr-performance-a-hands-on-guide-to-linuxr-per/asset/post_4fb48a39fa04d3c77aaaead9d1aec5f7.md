
## 9.6. Optimizing Memory Usage

Often, it is common that a program that uses a large amount of memory can cause other performance problems to occur, such as cache misses, translation lookaside buffer (TLB) misses, and swapping.

Figure 9-4 shows the flowchart of decisions that we will make to figure out how the system memory is being used.

Figure 9-4.

Go to Section 9.6.1 to start the investigation.

## 9.6.1. Is the Kernel Memory Usage Increasing?

To track down when using the system's memory, you first have to determine whether the kernel itself is allocating memory. Run `slabtop` and see the total of the kernel's memory is increasing. If it is increasing, jump to Section 9.6.2.

If the kernel's memory usage is not increasing, it may be a particular process causing the increase. To track down which process is responsible for the increase in memory usage, go to Section 9.6.3.

## 9.6.2. What Type of Memory Is the Kernel Using?

If the kernel's memory usage is increasing, again run `slabtop` to determine what type of memory the kernel is allocating. The name of the slab can give some indication about why the memory is being allocated. Through web searches, by searching the kernel source for the name of slab and determining which subsystem it is used in, it may become clear why it is allocated. After you determine which subsystem is allocating all that memory, try to tune the amount of maximum memory that particular subsystem can consume, or reduce the usage of that subsystem.

Go to Section 9.9.

## 9.6.3. Is a Particular Process's Resident Set Increasing?

Next, you can use `top` or `ps` to see whether a particular process's resident set size is increasing. It is easy to add `rss` to the field of output of `top` and sort by what type of memory is used. If a particular process is increasingly using memory, for what the application is using, go to Section 9.6.6. If no particular process is using more, go to Section 9.6.4.

## 9.6.4. Is Shared Memory Usage Increasing?

Use `ipcs` to determine whether shared memory is being used. If it is, go to Section 9.6.5 to determine which processes are using the memory. Otherwise, have a system memory leak not covered in this. Go to Section 9.9.

## 9.6.5. Which Processes Are Using the Shared Memory?

Use `ipcs` to determine processes processes are using shared memory. After the processes that use the shared memory have been identified, investigate the individual processes to determine why the memory is being used for each. For example, look in the application's source code for calls to `shmget` and `shmat` (to attach to it). Read the application documentation and look for options that can reduce the usage of shared memory.

To reduce shared memory usage and go to Section 9.9.

## 9.7. Optimizing Disk I/O Usage

When you determine that disk I/O is a problem, it can be helpful to determine which application is causing the I/O.

Figure 9-5 shows the steps we take to determine the cause of disk I/O usage.

Figure 9-5.

![](img/e2cf6437fe9be84e01517553c4bb6a79_94_0.png)

To begin the investigation, jump to Section 9.7.1

## 9.8. Optimizing Network I/O Usage

When you know a problem is happening, Linux provides a set of tools to determine which applications are involved. However, when you are connected to external machines, the fix to a network problem is not always within your control.

Figure 9-6 shows the steps that we take to investigate a network performance problem.

![](img/e2cf6437fe9be84e01517553c4bb6a79_97_0.png)

To start the investigation, continue to Section 9.8.1.

## 9.8.1. Is Any Network Device Sending/Receiving Near the Theoretical Limit?

The first thing to do is use ethtool to determine what hardware speed each Ethernet device is set to. If you record this information, you investigate whether any of the network devices are saturated. Ethernet devices and/or switches can be mis-configured, ethtool shows what speed each Ethernet device is, use iptraf or ifconfig to determine the amount of traffic that is flowing over each interface. If the network device appears to be saturated, go to Section 9.8.3; otherwise, go to Section 9.8.2.

## 9.8.2. Is Any Network Device Generating a Large Number of Errors?

Network traffic can also appear to be slow because of a high number of network errors. Use ifconfig to determine whether any of the interfaces are generating a large number of errors. A large number of errors can be the result of a mismatched Ethernet card / Ethernet switch connection. Contact your network administrator, search the Web for similar problems, or e-mail questions to one of the Linux networking specialists.

Go to Section 9.9.

## 9.8.3. What Type of Traffic Is Running on That Device?

If a particular device is serving a load of data, use iptraf to track down what types of traffic that device is sending and receiving. When you know the type of traffic that the device is handling, advance to Section 9.8.4.

## 9.8.4. Is a Particular Process Responsible for That Traffic?

Next, we want to determine whether a particular process is responsible for that traffic. Use netstat -p to switch to see any process is handling the traffic that is flowing over the network port.

If an application is responsible, go to Section 9.8.6. If none are responsible, go to Section 9.8.5.

## 9.8.5. What Remote System Is Sending the Traffic?

If no application is responsible for this traffic, some system on the network may be bombarding you with unwanted traffic. To determine which system is sending this traffic, use iptraf or etherpepe.

## 9.9. The End

When you finally arrive here, your problem may or not be solved, but you will have a lot of information characterizing it. Search the Web and newsgroups for similar problems. E-mail developers to see how they resolved it. Try a solution and see whether the system’s or application’s behavior changed.

## 9.10. Chapter Summary

This chapter provided a method for using the Linux tools together to track down different types of problems. Although it is not possible to capture every type of problem that could go wrong, this methodology helps you find some of the more common. In addition, if the problem that you face is not covered here, the data that you collect will still be useful because it might open up different areas.

The next few chapters show this method being used to find performance problems on a Linux system.

- Use this chapter as a template for tracking down a CPU-related performance problem.

## 10.1. CPU-Bound Application

In this chapter, we investigate an application that is CPU-bound. It is important to be able to optimize CPU-bound application because it is one of the most common problems. It is also usually the final frontier for a heavily tuned application. As the disk and network bottlenecks are removed, the application becomes CPU-bound. In addition, it is often easier to buy faster disks or more memory than to upgrade a CPU, so if a process is CPU-bound, it is an important skill to be able to hunt down and fix a CPU performance problem rather than just buy a new system.

## 10.2. Identify a Problem

The first step in a performance hunt it to identify a problem to investigate. In this case, I chose to investigate a performance problem that crops up when using GIMP, an open-source image-manipulation program. GIMP can slice and dice various aspects of an image, but it also has a powerful set of filters that can warp and change an image in a variety of ways. These filters can change the appearance of the image based on some complicated algorithms. Typically, the filters take a long time to complete and are very CPU-intensive. One of the filters in particular, Van Gogh (LIC), takes an input image and modifies it so that it looks like a painting done in the style of Van Gogh. This filter takes a particularly long amount of time to complete. The amount of time to complete depends on the size of the image, the machine's CPU speed, and the values of the parameters passed into the filter.
