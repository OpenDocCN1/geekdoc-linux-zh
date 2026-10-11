The following session shows how to compile and to start the server in the background:

```
$ make rnperv
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rnperv.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rnpeng.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rnkad.d.c
gcc rnperv.o rnpen.g.o rnkad.d.o -o rnperv -lgmp
$ ./rnperv \'*;0090' &
[2] 915
$
```

After the server has been started, you can use telnet from multiple xterm windows to try out the server simultaneously. If you are not running the X Window system, you can use various virtual console sessions to accomplish the same effect.

The principle changes to the module are as follows:

+   - The ` <sys/wait.h> ` and ` <signal.h> ` include files were added in lines 16 and 17.
+   - A signal handler for **SIGCHLD** was added to lines 34 to 45.
+   - A process ID variable **PID** was declared in line 74.
+   - The **SIGCHLD** signal handler was installed at line 79.
+   - A call to **fork(2)** was added in lines 139 to 147.
+   - A call to **exit(2)** was added at line 189.

# Understanding the Overall Server Process

The basic main program of the server now functions as follows:

+   1. A signal handler for **SIGCHLD** is installed at line 79. This will play a role for terminated processes, which will be discussed later.
+   2. A server address and socket are created (lines 85 to 112).
+   3. The socket is converted to a listening socket (lines 117 to 119).
+   4. The main loop begins (line 124).
+   5. The server blocks its execution until a client connects (lines 128 to 133).
+   6. The **fork(2)** function is called in line 139.
+   7. If step 6 fails, the value –1 is returned by **fork(2)** and the server closes the connected socket c (line 141). Then the loop repeats with step 5.