For a low-volume Web server, you can probably leave the parameters alone that support the MPM feature. You will probably have enough processes to handle your incoming requests, but not so many that they will be a drain on your server. However, if your server needs to serve up lots of content consistently, or needs to respond occasionally to large spikes of requests, you should consider tuning the MPM-related parameters in the `httpd.conf` file.

Here are a few issues to consider if you want to change any of the MPM-related parameters:

+   * **RAM is critical** — Every process and thread that is active consumes some amount of memory. If the number of active processes and threads goes beyond the amount of RAM you have, your computer will begin to use swap space and performance will degrade quickly. Make sure this is enough RAM on your system to handle the maximum number of server processes and threads you expect to run on your Apache Web server.
+   * **Configure for maximum load** — Apache is able to create new server processes and threads as they are needed. You don’t need to have the maximum number of processes and threads available at all times. Instead, you can configure the maximum number of servers and threads that Apache can dynamically add as demand on the server requires.
+   * **Configure for performance** — Performance degrades when Apache has to start a new thread (small amount), start a server process (greater amount), or use swap space (greatest amount). In the perfect world, the exact number of servers you need should be the default number of servers running, with a few spares to handle reasonable spikes. If response is critical, you might opt to have more servers running than you need so that performance isn’t hurt when spikes come.

When Apache starts up, it launches a set number of `httpd` server processes (one parent and multiple child `httpd` processes) to handle incoming requests for content for the Web server. Parameters for defining how many `httpd` server processes are available include those that set:

+   * How many child server processes should be started by the parent `httpd` server (`StartServers`)
+   * The minimum number of server processes kept spare (`MinSpareServers`)
+   * The maximum number of server processes kept spare (`MaxSpareServers`)
+   * The maximum value `MaxClients` can be over the life of the server (`ServerLimit`)
+   * The maximum number of server processes allowed to start (`MaxClients`)
+   * The maximum number of requests a process can serve (`MaxRequestsPerChild`)

Parameters for defining how many threads are available for each `httpd` server process include those that set:

+   * The minimum number of spare threads that should always be available, after which more will be created (`MinSpareThreads`)
+   * The maximum number for spare threads, after which active threads will be deleted to get back to the number of threads per child (`MaxSpareThreads`)