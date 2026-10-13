# # The Solaris Multithreaded Process Architecture

The process was one of the two fundamental abstractions on which the original Unix system was built (the other was the *file*). Processes were the basic unit of scheduling and execution on Unix systems. Traditional implementations provided facilities for the creation, prioritization, scheduling, managing, and termination of processes. Some primitive commands and utilities existed for process monitoring (e.g., the ps(1) command), and cryptic debugging facilities allowed for setting breakpoints and stepping through process execution.

In this chapter, we discuss the Solaris process model, the process execution environment, and the multithreaded process architecture, including processes, lightweight processes, and kernel threads. We also cover other topics directly related to the kernel’s process model: procfs, signals, process groups, and session management.

# ## 8.1 Introduction to Solaris Processes

The Solaris kernel provides support for an entity known as a *process*, and the kernel maintains a systemwide *process table*, whereby each process is uniquely identified by a positive integer called the process identification number (PID). The ps(1) command provides a point-in-time snapshot, taken as specified by the ps(1) command options, of the kernel’s process table, providing process names, PIDs, and other relevant data about the processes.