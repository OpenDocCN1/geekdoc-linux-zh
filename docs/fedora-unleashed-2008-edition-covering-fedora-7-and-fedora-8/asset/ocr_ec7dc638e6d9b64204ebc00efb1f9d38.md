# CHAPTER 11
Automating Tasks

**I**n this chapter, you will learn about the three ways to automate tasks on your system: making them services that run as your system starts, making them services you start and stop by hand, and scheduling them to run at specific times.

After you turn on the power switch, the boot process begins with the computer executing code stored in a chip called the BIOS; this process occurs no matter what operating system you have installed. The Linux boot process begins when the code known as the boot loader starts loading the Linux kernel and ends only when the login prompt appears.

As a system administrator, you will use the skills you learn in this chapter to control your system’s services and manage runlevels on your computer. Understanding the management of the system services and states is essential to understanding how Linux works (especially in a multi-user environment) and will help untangle the mysteries of a few of your Fedora system’s configuration files.

Furthermore, a good knowledge of the cron daemon that handles task scheduling is essential for administrators at all skill levels.

In this chapter, you’ll take your first steps in shell scripting, but if you want to take it further, Chapter 33, “Writing and Executing a Shell Script,” is dedicated exclusively to programming shell scripts. These are preset lists of commands that you want to execute all at once, so putting them in a shell script means you can just type the name of the script and all the commands run in sequence. For now, though, we’re more interested in having things done automatically for us *without* much user intervention.

# IN THIS CHAPTER

+   - Running Services at Bootup
+   - Troubleshooting Runlevel Problems
+   - Starting and Stopping Services Manually
+   - Scheduling Tasks
+   - Basic Shell Control
+   - Reference