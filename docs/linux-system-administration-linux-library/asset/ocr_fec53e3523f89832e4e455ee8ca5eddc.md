# Chapter 3 Linux Files and Processes

Once again, use Ctrl+D to terminate input. Now when the system load drops below 0.8,
the backup will start.

# Daemons

Daemons are server processes. These processes run continuously in the background
until the service they represent is called. For instance, httpd (the Apache Hypertext
Transfer Protocol daemon) is a standalone Web server service. It is typically started
at boot time but spends most of its time monitoring the port assigned to Apache, looking-or work. When data comes in port 80 (Apache's default port), httpd picks up
the traffic and processes it as appropriate. When the job is done, it returns to
a listening mode.

A special daemon exists to monitor ports for other daemons, which have been
assigned to it. This daemon, traditionally called inetd, replaced by xinetd in Red
Hat 7.0, is referred to as a TCP/IP server. It is started at bootup, and listens to
the ports assigned the processes that are listed in the /etc/xinetd.conf file (or /etc/
xinetd.conf, for xinetd). Chapter discusses daemons and servers in more
detail.

# Parent Processes and Their Children

When a process needs to perform several functions in order to complete its task, it
cannot exit until all of the functions are finished. This means that if a system needs
to several database queries to complete a task, it might not update the screen
until all of the queries have been completed. In order to prevent such an obvious lag,
the parent process can initiate child processes to complete the subtasks in a more
expedient manner by performing as many of them as possible simultaneously. The
creation of child processes is called forking. Each child process is assigned a new
PID, but also retains its parent's ID as the PPID. This helps you track which process
called child process. The child process is a duplicate of the parent process,
heriting nearly all of its parent's environment with the exception of its PID. The
child then uses the exec command to replace itself in memory with the binary code
of a program that can perform the requested function. When the replacement program finishes its task, it exits.

Listing 3.4 shows an excerpt from the table of processes as output by the ps -ajx
command.