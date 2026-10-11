![](bbox=[0.83, 0.04, 0.99, 0.17])

# Managing Linux Processes

In this chapter, you will learn about

+   - Understanding how Linux handles processes
+   - Managing running processes
+   - Scheduling processes

You've learned a great deal about Linux so far in this book. We started off easy, learning about the historical origins of Linux and the different roles it can play in your organization. As we've progressed through each chapter, we've been introduced to increasingly more challenging Linux concepts and skills. In the last chapter, we really ratcheted things up when we talked about managing kernel modules. In this chapter, we're going to look at how the Linux operating system handles executable programs and scripts when they are run. Then we'll spend some time learning how to manage executables while they are running on the system.

![](bbox=[0.05, 0.54, 0.15, 0.64])

> **EXAM TIP** For your Linux+/LPIC-1 exam, you need to be very familiar with how Linux handles running processes. You need to understand the heredity of Linux processes as well as the difference between user processes and system processes (daemons). You should know how to use shell commands to view processes running on the system. You need to know how to run a process in the foreground and in the background. You should also know how to kill a process from the command line. You also need to know how to tell a process to continue running after the user that started it logs out. Finally, you need to know how to use at and cron to configure a service to run automatically in the future.

Let's begin this chapter by discussing how Linux handles processes.

# How Linux Handles Processes

The key to being able to effectively manage Linux processes is to first understand how processes function within the operating system. In this part of this chapter, we're going to discuss the following:

+   - What exactly is a process?
+   - The heredity of Linux processes

Let's begin by discussing what a process is.