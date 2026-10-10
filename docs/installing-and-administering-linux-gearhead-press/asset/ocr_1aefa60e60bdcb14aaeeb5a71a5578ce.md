+   ■ Conversely, your output facilities (screen or printer) are overwhelmed by program or process output.

+   ■ The process or program is using too many system or network resources (such as memory, CPU usage, or bandwidth usage).

+   ■ The process or program is not behaving properly or predictably.

The first reason likely affects an advanced user or system administrator who might have altered the configuration of one or more systems and now finds that daemons or other background processes are no longer relevant to the system. The other reasons are pretty much self-explanatory.

# ### Termination Methods

Foreground processes run on the user’s terminal and can usually be terminated by some type of quit signal. The three most common methods are as follows:

+   ■ The Ctrl-C key sequence

+   ■ The *kill* command

+   ■ Powering the system down

The Ctrl-C key sequence is the most common method. It stops a foreground process and returns you to a shell prompt, generally a dollar sign ($) for users or a pound sign (#) for the administrator, root, and superuser. But remember that Ctrl-C does not work with man; use q or Ctrl-Z instead. Also, some shell scripts or other programs might ignore the quit signal.

In some cases where the processes ignore the common quit signals, you might have to enter the *kill* command, which we discuss in detail in the next section. You always have to use *kill* to terminate background processes.

Powering down a local system is a reasonably sure way of terminating foreground or background processes running on the system. You should always be concerned with the effects that suddenly powering down might have on individual files or programs, file systems, other system features or processes, and even other users, however. So powering down should be a last resort alternative.

# #### The kill Command

An ordinary user has the ability to kill any process that he or she has initiated. By comparison, a root user can kill *any* process. The syntax is