# Tuning Apache for Performance

Apache on Windows was multithreaded even before Apache 2.0. This is because Windows systems such as Windows 2000 and Windows NT perform better with threads than they perform with a bunch of child processes constituting a service.

On Windows systems, Apache runs using only two processes. A parent process monitors a child process, which is responsible for servicing all requests using multiple threads.

To control how many simultaneous requests Apache can serve under Windows, you need to tune the `ThreadsPerChild` directive. See Chapter 4 for details on this directive. This directive controls the number of threads that can be created by the sole Apache child process responsible for all requests. The default value of 50 should be fine for most sites.

If you require a higher response rate, make sure you have the appropriate system resources such as sufficient RAM and a fast CPU to backup your rate requirements. According to the source code for the `winnt_MPM` module, you should be able to set this to a maximum of 4096 threads. Most likely, a number below 256 is more appropriate for most Web sites.

The `MaxRequestsPerChild` directive limits the number of requests that a child process can handle (see Chapter 4 for details on this directive). Because a single child processes all the requests via threads under Windows, this directive should be either set to a very high number or to 0, which means the child process will never exit.

# Testing Apache Configuration

Whenever you change the `httpd.conf` file, you can run the following command from the Apache binary directory (`C:\Program Files\Apache Group\Apache` by default) to determine whether you have created any syntax errors.

```
Apache -t
```

You can also choose `Start\Programs\Apache httpd Server\Configure Apache Server\` Test Configuration option to do the same.

If an error is found, you can fix it before restarting the server with the `Apache -k restart` command.