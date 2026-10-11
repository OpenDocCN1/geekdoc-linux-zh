# ## What Exactly Is a Process?

So, what exactly is a “process”? This term tends to be used in a variety of different ways in the computing industry, so it can be difficult sometimes to nail down exactly what it means. In this part of this chapter, we’ll help you understand what a process is by discussing the following:

+   - Processes defined
+   - Types of processes

# ### Processes Defined

For our purposes here, a *process* is a program that has been loaded from a long-term storage device, usually a hard disk drive, into system RAM and is currently being processed by the CPU on the motherboard.

Many different types of programs can be executed to create a process. On your Linux system, the types of programs listed in Table 13-1 can be loaded into RAM and executed by the CPU.

Remember that the Linux operating system can run many processes “concurrently” on a single CPU. Depending on how your Linux system is being used, it may have only a few processes running at a given point in time or it may have hundreds of processes running concurrently.

**Table 13-1** Linux Programs That Can Create Processes

| **Type of Program** | **Description** |
| :--- | :--- |
| **Binary executables** | These are programs that were originally created as a text file using a programming language, such as C or C++. The text file was then run through a compiler to create a binary file that can be processed by the CPU. |
| | Remember when you learned how to install applications from source code in a previous chapter? You were using a compiler (gcc) to compile the text file you downloaded into a binary executable. |
| **Internal shell commands** | Some of the commands you enter at the shell prompt are actual binary files in the file system that are loaded and run by the CPU. For example, when you enter *rpm* at the shell prompt, you load the *rpm* binary file into memory. |
| | Other commands, however, are not binary executables. Instead, they are commands that are rolled into the shell program itself. For example, if you enter *exit* at a shell prompt, you are actually running an internal shell command. There is no executable file in the file system named “exit.” Instead, the computer code associated with the exit function is stored within the shell program code itself. |
| **Shell scripts** | These are text files that are executed through the shell itself. You can include commands to run binary executables within the text of any shell script. You will learn how to create shell scripts in a later chapter. |