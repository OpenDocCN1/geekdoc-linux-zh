Setting the close on exec flag is another one of the miscellaneous facilities provided by a call to fcntl(). The form of the call for setting the close on exec flag on a particular file descriptor (fd) is:

```
fcntl(fd, F_SETFD, FD_CLOEXEC);
```

Just to recap for a moment, when you want a running process to organize the execution of another program as part of its operation, the sequence of steps is as follows:

+   - The running process gets or generates the command that is to be executed.
- The process does a fork() system call. This starts up a new process which is a copy of, and runs concurrently with, the original process. The original process is called the parent and the new one is called the child.
- The child process now executes an exec() call which scraps the text and user data segments of the child process and replaces them with the text and user data in the command file that is to be run.

Two obvious questions arise on looking at this scenario. First, wasn't it rather a waste of effort creating the child process as an exact duplicate of the parent only to scrap that immediately and replace it with a new program? And, second, what does the parent process do while the child process is executing?

Taking the questions in that order – Linux implements its fork() system call in a very efficient way. In effect, Linux cheats. It doesn't really make a full copy of the process at all, it just has two sets of pointers, one for each process, that both point to the same real text and data segments. In the case of the text segment, this doesn't matter because the segment is read-only anyway. In the case of the data segments, however, it decidedly does matter because these are supposed to be a pair of independent processes. But, thinking about it for a moment, as long as the two processes only read data from the data segments and don't do any writing of new values, then neither process will know that the cheat is taking place. In order for this scheme to work completely, all Linux has to do is to spot when one of the two processes tries to write something to one of the data segments and create a copy of just that little bit when it is needed. This technique is called copy on write.

In essence, any area that gets written to by either process gets copied so that both processes then have their own copies of those areas. If the child process immediately performs an exec() call, then very little of the shared data segment space will have been copied before the exec() takes place – a huge saving in time and resources.

# 16.4 wait and exit System Calls

The answer to the question of what the parent process does while the child process runs is quite simple – either it waits for the child process to terminate or it just gets on with whatever else it needs to do.