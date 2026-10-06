
## 8.3. Chapter Summary

This chapter provided a grab of Linux utility tools that are useful when investigating a performance problem. It introduced tools such as bash, tee, and script, which automate the display and collection of performance data. It also introduced gnumeric, a tool that can graph and analyze the results of text-based performance tools. It then investigated ldd and objdump, which can be used to track down which library a function is part of. It then described `gdb`, a tool that can investigate the execution and runtime information of running applications. Finally, this chapter described `gcc` tools, such as `oprofile`, to map events back to a specific source line, and binaries with symbolic debugging information that help other performance tools.

In the upcoming chapters, we put together all the tools presented so far and solve some real-life performance problems.

## Chapter 9. Using Performance Tools to Find Problems

This chapter contains a method for using the previously presented performance tools together to narrow down the cause of a performance problem.

After reading this chapter, you should be able to:

- Start with a misbehaving system and use the Linux performance tools to track down the misbehaving kernel functions or applications.
- Start with a misbehaving application and use the Linux performance tools to track down the misbehaving functions or source lines.
- Track down excess usage of the CPU, memory, disk I/O, and network.

## 9.1. Not Always a Silver Bullet

This chapter assumes that it is possible to solve a performance problem by changing software. Tuning an application or system to achieve a target performance goal is not always possible. If tuning fails, it may require a hardware upgrade or change. If the capacity of the system is maxed out, performance tuning only helps to a certain extent.

For example, it may be necessary (or even cheaper) to just upgrade the amount of system memory rather than track down which applications are using system memory, and then tune them so that they reduce their usage. The decision to just upgrade the system hardware rather than track down and tune a particular performance problem depends on the problem and is a value judgment of the individual money-wise (to buy new hardware). Which option is cheaper, either time-wise (to investigate the problem) or money-wise, in some situations, tuning will be the preferred or only option is what this chapter describes.

## 9.2. Starting the Hunt

After you decide to start optimizing something on Linux, you first have to decide what you are going to optimize. The method used in this chapter covers some of the more common performance problems and an example shows how you use the previously presented tools together to solve a problem. The next series of sections helps guide you in your discovery of the cause of a performance problem. In many sections you are asked to run various performance tests and jump to different sections in this chapter based on the results. This helps to pinpoint the source of the problem.

As stated in previous chapters, it is a good idea to save the results of each test that you perform. This enables you to review the results later and even to send the results to someone else if the investigation is inconclusive.

Let's get started.

When investigating a problem, it is best to start with a system that has as little unrelated programs running as possible, so close or kill any unneeded applications or processes. A clean system helps eliminate the potentially confusing interference caused by any extraneous applications.

If you have a specific application or program that is not performing it as it should, jump to Section 9.3. If no particular application is sluggish and, instead, the entire Linux system is not performing as it should, jump to Section 9.4.

## 9.3. Optimizing an Application

When optimizing an application, several areas of the application's execution may present a problem. This section directs you to the proper section based on the problem that you are seeing.

Figure 9-1 shows the steps that we will take to optimize the application.

Figure 9-1.

![](img/e2cf6437fe9be84e01517553c4bb6a79_82_0.png)

## 9.4. Optimizing a System

Sometimes, it is important to approach a misbehaving system and figure out exactly what is slowing down everything.

Because we are investigating a system-wide problem, the cause can be anywhere from user applications to system libraries to the Linux kernel. Fortunately, with Linux, unlike many other operating systems, you can get the source for most all applications on the system. If necessary, you can fix the problem and submit the fix to the maintainers of that particular piece. In the worst case, you can run a fixed version locally. This is the power of open-source software.

Figure 9-2 shows a flowchart of how we will design a system-wide performance problem.

Figure 9-2.

Go to Section 9.4.1 to begin the investigation.

### 9.4.1. Is the CPU-Bound?

Use top.procinfo, or mpstat to determine where the system is spending its time. If the entire system is spending less than 5 percent of the total time in idle and wait modes, your system is CPU-bound. Proceed to Section 9.4.3. Otherwise, proceed to Section 9.4.2.

### 9.4.2. Is a Single Processor CPU-Bound?

Although the system as a whole may not be CPU-bound, in a symmetric multiprocessing (SMP) or hyperthreaded system, an individual processor may be CPU-bound.

Use top or mpstat to determine whether an individual CPU has less than 5 percent in idle and wait modes. If it does, one more CPU is CPU-bound; in this case, go to Section 9.4.4.

Otherwise, CPU is CPU-bound. Go to Section 9.4.7.

### 9.4.3. Are One or More Processes Using Most of the System CPU?

The next step is to figure out any particular application or group of applications is using the CPU. The easiest way to do this is to run top. By default, top sorts the processes that use the CPU in descending order. top reports CPU usage for a process as the sum of user and system time. For example, if an application spends 20 percent of the CPU in user space code, and 30 percent in system code, top will report that the process has consumed 50 percent of the CPU. Sum up the time of all. If that is significantly less than the system-wide percentage, the kernel is doing significant work that is not on the behalf of applications.

Otherwise, go to Section 9.4.3. (Note: Context suggests 9.4.4, but keeping text logic) or de-duplicate to where the process is identified.

### 9.4.4. Are One or More Processes Using Most of the System CPU?

The next step is to figure out any particular application or group of applications is using the CPU. The easiest way to do this is to run top. By default, top sorts the processes that use the CPU in descending order. top reports CPU usage for a process as the sum of user and system time. For example, if an application spends 20 percent of the CPU in user space code, and 30 percent in system code, top will report that the process has consumed 50 percent of the CPU. Sum up the time of all. If that is significantly less than the system-wide percentage, the kernel is doing significant work that is not on the behalf of applications.

Otherwise, go to Section 9.4.3. (Note: Context suggests 9.4.5) or de-duplicate to where the process is identified.

## 9.5. Optimizing Process Usage

When a particular process has been determined to be a bottleneck, it is necessary to determine where (and why) it is spending its time.

Figure 9-3 shows the method for investigating process usage.

Figure 9-3.

Go to Section 9.5.1 to begin the investigation.

### 9.5.1. Is the Process Spending Time in User or Kernel Space?

You can use the time to determine whether an application is spending time in kernel or user space. profiling at process shows where the time is spent.

If the application is spending a significant amount of time in kernel space (greater than 25 percent), go to Section 9.5.2. Otherwise, go to Section 9.5.3.

### 9.5.2. Which System Calls Is the Process Making, and How Long Do They Take to Complete?

Next, trace to see which system calls are made and how long they take to complete. You can also run profile to see which kernel calls are being made. It may be possible to increase performance by minimizing the number of system calls made or changing system calls made on behalf of the program. Some of the calls may be unexpected and a trace of the application's calls helps.

### 9.5.3. In Which Functions Does the Process Spend Time?

Next run profile on the application cycle to determine which functions are using all CPU cycles (that is, which functions are spending the application time).

Keep in mind that profiling shows how much time was spent in process, profiling at the function level, is not clear whether a function is hot because it is called very often or whether it takes a long time to complete.

One way to determine which case is true is use a source-level annotation from profile and look for instructions/source lines that should have little overhead (as assignments). The number of samples that we will the number of functions that was called relative to other high-cost sources. This is only approximate because profile samples only the CPU, and out-of-order processes can miscarry some issues.

It is also helpful to call a graph of functions to determine how the hot functions are being called. To do this, go Section 9.5.4.

### 9.5.4. What Is the Call Tree to the Hot Functions?

Next, you can find how the time-consuming functions are being called. Running the application with gprof can show the call tree for function. If the time-consuming functions are in a library, you can use trace to see which. Finally, you can use newer versions of profile
