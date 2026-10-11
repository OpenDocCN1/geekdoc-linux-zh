+   17. Press p and then enter your password.
+   
+   18. Select the appropriate GRUB menu item to boot the system.

# Managing Linux Runlevels

If you’ve worked with Linux before, you may have heard the term runlevel used. I’ve noticed that the concept of a runlevel is difficult for many new Linux users to understand. In this part of this chapter, we’ll review what a runlevel is and how you can manage runlevels on your system. The following topics will be covered:

+   - How runlevels work
+   - Managing runlevels and init scripts

Let’s begin by discussing how runlevels work.

# How Runlevels Work

To manage a Linux system, you need to have a sound understanding of how runlevels work. In this part of this chapter, we’ll discuss the following:

+   - What is a runlevel?
+   - Defining runlevels in /etc/inittab

Let’s begin by discussing what a runlevel is.

# What Is a Runlevel?

So what exactly is a runlevel? It sounds complicated, but when you get right down to it, it really isn’t. A runlevel represents one of several different modes that your Linux system can run in. A runlevel on a Linux system is similar, in many ways, to a startup mode on a Windows system. If you’ve used Windows, you know that you can press the F8 key during system boot and select one of several startup modes. For example, if you’re having trouble with a particular device or driver in your Windows system, you can boot it in Safe Mode, which will load the operating system with only a minimal set of drivers so that you can troubleshoot the problem.

Linux runlevels are similar. Like Windows startup modes, Linux runlevels allow you to specify the mode in which you want your system to run. Linux uses seven default runlevels that you can choose from, as shown in Table 6-4.

As you can see in Table 6-4, there are many differences between Linux runlevels and Windows startup modes. First of all, switching to runlevel 0 actually halts the system while switching to runlevel 6 reboots the system. In addition, you can specify a default runlevel that your system will boot into each time it’s turned on. You can even dynamically switch between runlevels while the system is running. You can’t do that with Windows!

These runlevels are defined through the /etc/inittab file. Let’s review how this file works next.