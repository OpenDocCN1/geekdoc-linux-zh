default behavior (all) requires that the client pass the address access restriction and enter a valid username and password. With the any option, the client is granted access if the user either passes the host restriction or enters a valid username and password. This directive can be used to restrict access to an area by using passwords, while simultaneously giving access to all clients from a particular IP address pool (that is, a set of IP addresses) without requiring them to enter passwords.

# ScriptInterpreterSource

The `ScriptInterpreterSource` directive allows you to specify how Windows finds the interpreter for a script. Normally, the script interpreter is detected using the `#!` line found in a script. However, setting this directive to registry will force Windows to lookup the registry for the script's extension to find the associated program (that is, interpreter) for it.

+   Syntax: `ScriptInterpreterSource Registry | Script`
+   Default setting: `ScriptInterpreterSource script`
+   Context: directory, .htaccess

# MPM threaded-Specific Directives

This is like prefork MPM but instead of each child process having a single thread, each child process is allowed to have a specified number of threads. Because threads are more resource efficient than processes, this MPM is very scalable. Each thread within a child process can service a different request.

A process is added or removed by monitoring its spare thread count. For example, if a process has less than the minimum number of spare threads, a new process is added. Similarly, when a process has a maximum number of idle threads, it is killed.

> All processes run under the same user and group ID assigned to Apache server.

# CoreDumpDirectory

The `CoreDumpDirectory` directive sets the directory that Apache tries to switch to before crashing and dumping the core (memory image of the server) file. The default location is the directory specified by the `ServerRoot` directive.

+   Syntax: `CoreDumpDirectory directory_path`
+   Default setting: Server's root directory
+   Context: Server config