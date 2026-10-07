# Chapter 3: Compound Command Syntax 119

a) How many jobs were there, and what were their numbers?

LAB 3.1

b) Run the command line again. Did you get the same job numbers?

The other numbers are process ids.

c) Did you get the same set of process ids the two times you ran the command?

> When the shell runs an external command, it normally does so by telling the operating system's kernel to create a process to run the command. The shell itself runs as a process, and built-in commands are run as part of the shell's process. Using processes judiciously can affect the efficiency of your scripts greatly.

![](bbox=[0.025, 0.506, 0.113, 0.556])

The term job refers to the processes that you can control using the shell. For example, putting an ampersand at the end of a command creates a background job, a process that runs in parallel with the shell itself.

a) How many background jobs did you create by entering the preceding command line?