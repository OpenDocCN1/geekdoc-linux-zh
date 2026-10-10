# ## Process Environments

A process is a single program or task running in its own virtual address space. A command or a job can consist of many processes, but (contrary to some opinions) a process is not necessarily the same as a command or a job. Very simple commands, however, can be considered single processes.

From a strict technical interpretation, a program is just a set of instructions, but a process is a dynamic operation that uses the running system’s resources. As we discussed before, when you log in, Linux places you in your home (file) directory and initiates a program called a shell. The shell itself is a process. After that, whenever you invoke commands or applications, you are initiating them from within the shell (that is, from within the shell process).

In Linux, you can run more than one process at a time, and you can run several copies of the same program simultaneously. You can also track the environments of all the processes while they run. Table 12.1 summarizes the environment, which consists of variables and parameters that a typical process might require to run. Some processes require fewer variables and parameters; others require more.

We have already mentioned that the shell is a process. Example 12.1 shows you how to check the process ID, or PID, of the shell process.

# **Table 12.1** Process Environment

| **FIELD** | **EXPLANATION** |
| :--- | :--- |
| Terminal (TTY) | Terminal ID from which the process was launched |
| Open files | Files the process is using |
| Current directory | The directory from which the process was invoked |
| User ID (UID) | ID of the user who invoked the process |
| Group ID (GID) | ID of the group to which the user belongs |
| Process ID (PID) | A unique number that the kernel randomly assigned to the process |
| Parent process ID (PPID) | A unique number randomly assigned by the process that launched the subject process, if applicable |
| Flags | Any options and arguments appended to the command that launched the process |