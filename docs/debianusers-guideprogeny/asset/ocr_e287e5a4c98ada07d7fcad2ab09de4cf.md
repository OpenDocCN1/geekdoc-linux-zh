# Stopping a Process From the Command Line

You can stop a process from the command line in three ways:

+   Identifying it by ID.
+   
+   Identifying it by the command that starts it.
+   
+   Identifying it by a file that uses it.

# Stopping a Process Identified by ID

Type: kill PROCESS_IDS.

Unless you are root user, you can only kill processes that you started.

> **Warning**
> 
> Closing a process can crash your system or cause other problems.

# Stopping a Process Identified by Name or Files

Type: killall OPTIONS COMMAND.

Unless you are root user, you can only kill processes that you started.

> **Warning**
> 
> Closing a process can crash your system or cause other problems.

# Stopping a Process Identified a File Using It

Type: killall OPTIONS FILE.

A name with a forward slash in it is read as a file name. All processes that use that file are closed.

Unless you are root user, you can only kill processes that you started.