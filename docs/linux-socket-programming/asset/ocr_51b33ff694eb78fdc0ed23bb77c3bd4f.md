![](bbox=[0.17, 0.06, 0.82, 0.55])

During a task switch, the operating system replaces the current page table entries with those of the incoming task. This overhead can take several CPU cycles. You may see task switching overhead between 1μs and 0.1ms, depending on the microprocessor and its clock rate. That can be a long time—especially when Linux task switching is 100 times per second (every 10ms). Each task gets a portion of the CPU’s time, and part of this allocation is the task switch itself.

On some UNIX versions, threads run faster because the task switcher has to flush fewer page table entries. The 2.0 and 2.2 Linux kernel versions showed a nearly identical switching time. This similarity is due to the finely tuned switching algorithms.

Linux and other operating systems also support symmetric multiprocessing. If you write your programs to support multitasking, you get an automatic turbo charge when they run on symmetric multiprocessors. Basically, the rules are the same in Linux, only there are two or more processors to run the tasks. (At the time of this writing, Linux supports a maximum of 16 symmetric CPUs.)

# When to Use Multitasking

When should you use multitasking? Generally, a user should always have control over a program. Sometimes the program has to wait for other operations to complete, so it must use multitasking to interact with the user while waiting for the other operations. In the same way that Netscape allows you to access its menus while downloading a Web page, the parent program you design should