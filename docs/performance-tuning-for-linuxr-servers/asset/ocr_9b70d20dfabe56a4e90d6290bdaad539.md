are depending on this thread to run before they can proceed. Otherwise, it is not that harmful.

+   * *MW* for monitor wait, which means that the thread is queued in a monitor of a Java object. Remember that all Java objects have their own monitor. A thread would get in this state if it enters a *synchronized* method or block and another thread has already gotten the "right" to execute the synchronized method or block. Unless that executing thread leaves the synchronized method or block, no other thread waiting on it can proceed. Thus, this is the highest possible cause of bottlenecks.

We will perform one test run with 10 concurrent users. During that time, we will take note of the process ID of the Java process (which corresponds to the application server). During the run, we will issue the following command:

```
# kill -3 process id
```

You can check the process ID of the application server by looking for Java processes using the *ps* command. Some application servers log their process ID when they are started. Although the command says "kill," it does not terminate the process. Instead, it produces a thread dump and saves it on a file of the form *javacorexxxxxx.txt*. Note that thread dumps are not part of the JVM or Java Specifications, so different JVM implementations might use different filenaming schemes. We typically issue this command in succession (three to five times) to get more than one thread dump and to monitor the progress of the threads by checking to see if they ever change their state at all.

> Never take a thread dump if you are running a test run and getting performance data. Thread dumps slow down the JVM and thus affect its performance.

We took a thread dump of the application server while running a test with 10 concurrent users. Thread dumps can be huge files, depending on the number of threads in the JVM. Thread dump output also provides information about the system and the JVM.

Although this chapter does not cover how to interpret thread dump output, for the purposes of this case study, we are only interested in finding out if any threads are in the *MW* statespecifically, on the database routines.

*Figure 22-7* shows a snippet of thread information from the thread dump that we took. Note that we show only the topmost part of the stack trace because the stack traces are really deep. The thread in *Figure 22-7* is just one of the *Servlet.Engine. Transports threads* (threads are *pooled* in this application server). This thread is basically a worker thread that receives the request from the plug-in and executes it. As you can see, the state of the thread is R. The top of the stack trace tells us that this thread is in the JDBC code, which communicates with the local database client. The database client communicates with the remote database server.

# **Figure 22-7. A snippet of a thread stack trace taken from a thread dump.**

![](bbox=[0.42, 0.85, 0.58, 0.87])