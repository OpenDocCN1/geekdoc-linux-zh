# 4.1.2.2 Automatic processes

Automatic or batch processes are not connected to a terminal. Rather, these are tasks that can be queued into a spooler area, where they wait to be executed on a FIFO (first-in, first-out) basis. Such tasks can be executed using one of two criteria:

+   - At a certain date and time: done using the at command, which we will discuss in the second part of this chapter.

+   - At times when the total system load is low enough to accept extra jobs: done using the **batch** command. By default, tasks are put in a queue where they wait to be executed until the system load is lower than 0.8. In large environments, the system administrator may prefer batch processing when large amounts of data have to be processed or when tasks demanding a lot of system resources have to be executed on an already loaded system. Batch processing is also used for optimizing system performance.

# 4.1.2.3 Daemons

Daemons are server processes that run continuously. Most of the time, they are initialized at system startup and then wait in the background until their service is required. A typical example is the networking daemon, xined, that is started in almost every boot procedure. After the system is booted, the network daemon just sits and waits until a client program, such as an FTP client, needs to connect.

# 4.1.3 Process attributes

A process has a series of characteristics, which can be viewed with the ps command:

+   - The process ID or PID: a unique identification number used to refer to the process.

+   - The parent process ID or PPID: the number of the process (PID) that started this process.

+   - Nice number: the degree of friendliness of this process toward other processes (not to be confused with process priority, which is calculated based on this nice number and recent CPU usage of the process).

+   - Terminal or TTY: terminal to which the process is connected.

+   - User name of the real and effective user (RUID and EUID): the owner of the process. The real owner is the user issuing the command, the effective user is the one determining access to system resources. RUID and EUID are usually the same, and the process has the same access rights the issuing user would have. An example to clarify this: the browser **mozilla** in /usr/bin is owned by user *root*.