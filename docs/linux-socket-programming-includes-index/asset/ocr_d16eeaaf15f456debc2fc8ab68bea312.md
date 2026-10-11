```
```text
        int client = accept(sd, 0, 0);
        Child(client);  /*---Serve new Client---*/
      }
      else if ( pid > 0 )             /*---PARENT---*/
        ChildCount++;
      else                            /*---ERROR---*/
        perror("fork() failed");
      }
      else
        sched_yield();               /*---OR,  sleep(1)---*/
}
```
```

This reverses the order of the accept() and fork(): Instead of creating the process after a connection, this algorithm waits for the connection after creating the child process.

This code fragment may create 10 processes, for example. All the child processes enter the forever loop waiting for and processing connections. Assuming no connections are waiting, all 10 processes I/O block (sleep). When a connection arrives, all of the process wake up, but only one gets the connection. The remaining nine go back to sleep. This cycle continues indefinitely.

What happens if one of the child processes crashes or terminates? This is why the parent never makes the accept() system call. The parent’s primary role is to make sure that the correct number of children are always available.

At first, the parent creates the quota of child processes. When a child terminates, the signal handler picks up the notification and decrements the quota by one. When the parent resumes, it creates a new child. If the parent does not need to create more, it yields the timeslice to another task.

# Adapting to Different Load Levels

The parent’s primary responsibility is to make sure that enough child processes are available to serve the incoming connections. This responsibility must be balanced against your computer’s resource load. If you are not careful, the clients may begin to drop off due to timeouts because your server does not have enough listeners serving connections.

Using a dedicated number of listeners (servelts) forces a limit on the number of active connections. This is the primary restriction on having preforked servelts. Nevertheless, the idea of limiting the number of processes that your program creates and destroys is a good one. It lessens the turmoil on your process table and system resources. What might be a good way to minimize creation and destruction while meeting the needs of connecting clients?