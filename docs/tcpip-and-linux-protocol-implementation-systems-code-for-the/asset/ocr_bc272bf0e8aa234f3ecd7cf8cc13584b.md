# TCP/IP and Linux Protocol Implementation

inherit your parent's identity. To change identity, a process may set its user ID, although only to reduce the access rights that a child may obtain. This sounds draconian, but is in fact, quite general.

Linux also keeps track of time. This is fairly essential for a number of networking protocols, as well as being important for bookkeeping (e.g., file creation, and access modifications, process start, and system usage statistics).

There is a lot more context associated with a task that Linux manages in to keep life simpler for the application programmer.

For example, the filesystems provide a hierarchical organization of directories. This is useful for users and applications as a navigation aid. To help keep brief, the current working directory is part of the state associated with a process. In keeping with the simple (but effective) approach to control, UNIX allows a process to change its view of the root of the filesystem is. This allows processes to restrict childrens' views of things.

Processes start with three standard channels to the outside world: input, output, and errors. These are associated with the controlling terminal or tty. Pass these through to their children (of course a process is at liberty to detach from a controlling terminal so that it can run in background). A group of processes controlled by the same terminal are managed together. The idea of groups of processes is very useful in networking, since one can manage the state of the group, particularly through the use of signals.

Signals provide a way for the operating system to notify of a process an event. This originates from the requirement for raising exceptions (software interrupts) in a task: for an extreme example, many UNIX systems can use a signal to all processes when the power is about to die. Nowadays, signals are used for many asynchronous communications, alongside more normal file, pipe, and socket communication tools, of which we will see more.

The kernel and user process may use signals to communicate (albeit abruptly) with another process. If a process wishes to communicate in a civilized manner, with another process on the same machine, there are several choices. If the programmer wants a record of the communication, the simplest technique is to use files. UNIX does not restrict the reading and writing of files by default to a specific process, but there are tools to control access to files and provide synchronization. A more common technique is the use of a pair of file-like channels, called a pipe. Finally, the programmer might use full-fledged communications channels as a socket, which can be used for purely local, or inter-machine, inter-process communication.

To summarize, we can take the view from below as the operating system context, or the view from above, application/user context. The viewpoints are like a dual personality, or the subconscious and conscious.¹

> ¹A fanciful model of system calls might be the visual metaphor in Jean Cocteau's film of the Orpheus and Eurydice legend when the poet follows his true love into hell, by going through mirrors.