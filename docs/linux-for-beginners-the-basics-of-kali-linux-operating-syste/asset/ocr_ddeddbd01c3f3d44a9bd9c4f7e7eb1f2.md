the thread that was waiting to complete it may receive execution status. When creating a stream or joining it, if the stream cannot connect, it is called *disconnected* or detached. If the stream is not disconnected, it is called *Pluggable*, after which it is necessary to join them to stop memory leakage.

# Managing Processes In UNIX and Linux

# Image Of The Process

In UNIX systems, the process image contains the following components:

+   - Process control unit
+   - The code of the program executed by the process
+   - The process stack where temporary data is stored (procedure parameters, return values, local variables, etc.)
+   - Global data common to the whole process

# Identification Information And Process Security Attributes

The process identifier (PID) is unique throughout the system and is used to access this process. The init process identifier is always one. The process ID of the ancestor (ppid) is specified when it is created. If the ancestor of process P completes execution, the ancestor of that process automatically becomes init, so ppid for P will be unity.

With the process as fl' related set of security attributes.

+   - The real user and process group identifiers (uid, gid) correspond to the user who started the program, resulting in