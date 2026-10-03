# INTRODUCTION

This chapter covers Solaris processes—how to view processes, understanding the effects signals have on processes, and how to manage processes.

In addition to the test objectives outlined at the beginning of this chapter, I've included a section on syslog. Although syslog is an objective that's covered on the Part II exam, it fits well with the material in this chapter and did not warrant a chapter of its own.

# VIEWING A PROCESS

Solaris is a multitasking environment in which a number of programs run at the same time. Each Solaris program can start and stop multiple processes while it is running. A Parent process forks a child process, which in turn can fork other processes.

A process is a single program running in its own address space. A process under Solaris consists of an address space and a set of data structures in the kernel to keep track of that process. The address space is a section of memory that contains the code to execute a task. The kernel must keep track of the following data for each process on the system:

+   - Address space
- Current status of the process
- Execution priority of the process
- Resource usage of the process
- Current signal mask
- Ownership of the process

> NOTE
The term “fork” is used to describe a process started from another process. As with a fork in the road, one process turns into two. You'll also see the term “spawn” used—the two words are interchangeable.

A process is distinct from a job, command, or program that may be composed of many processes working together to perform a specific task. For example, a computer-aided design application is a single program. When this program starts, it spawns other processes as it runs. When a user logs into the program, it spawns yet other processes. Each process has a process ID associated with it and is referred to as a pid. You can monitor processes that are currently executing by using one of the commands listed in Table 9.1.