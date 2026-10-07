# Process Structures

# 265

![](bbox=[0.125, 0.093, 0.951, 0.442])

Figure 8.4 Conceptual View of a Process

To summarize the previous paragraphs: It is through the ELF file definition and format that the kernel and associated tools (compiler and linker) create a disk file that is an executable object which can be properly loaded into memory and turned into a process for scheduling and execution.

All of the process context, both hardware and software, is maintained in the data structures described in the sections that follow.

# 8.2 Process Structures

In this section, we take a look at the major data structures that make up the multithreaded process model in the Solaris kernel.

# 8.2.1 The Process Structure

The process structure, or proc structure, provides the framework for the creation and management of processes and threads in the Solaris environment. Figure 8.5 illustrates the big picture, showing the process structure with most of the structure members, along with all the other components that provide the entire process execution environment.