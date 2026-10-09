
```c
default: /* "impossible" case */
errno = 0;
EC_FAIL
}

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}
```

Both functions return true on success and false on error. The statusp argument gives the result for ready: CR_READY, CR_NOTREADY, or CR_EOF. For cget, the only possibilities are CR_READY and CR_EOF.

We’ve preempted the NUL byte as our empty-buffer indicator (EMPTY), which means that NUL bytes read by cready will be ignored. If this isn’t acceptable, a separate bool variable can be used as an empty-buffer flag.

Notice the way cready and cget shift back and forth between blocking and non-blocking input. Since we’re reading only one input stream, there’s no need to stay in the nonblocking state while we test for an available character, as we had to do in the first, inefficient, version of ready in Section 4.2.2. We revert to blocking and issue a read. After all, waiting for a character is what blocking means.

cready and cget are most useful when a program has some discretionary work to do, work that can be postponed if a character is ready. A good example is a program that uses Curses (Section 4.8). The way Curses works, all the screen output is held in a buffer until refresh is called to send it to the physical screen. This is time-consuming because refresh compares what is currently on the screen with the new image so as to minimize the number of characters transmitted. A fast typist can easily get ahead of the updates, especially if the screen must be updated on each keystroke, as it must with a screen editor. A neat solution is to call refresh from within the input routine, but only if input is not waiting. If input is waiting, then the user has obviously typed ahead without waiting for the screen to catch up, so the screen update is skipped. The screen will be updated the next time the input routine is executed, unless a character is waiting then too. When the user stops typing, the screen will become current. On the other hand, if the program can process characters faster than the typist types them, the screen will get updated with each keystroke.

This may sound complex, but by using functions we’ve already developed, it takes only a few lines of code:

```c
ec_false( cready(&status) )
if (status == CR_NOTREADY)
    refresh();
ec_false( cget(&status, &c) )
```

## 4.3 Sessions and Process Groups (Jobs)

This section explains sessions and process groups (also called jobs), which are mainly for use by shells.

### 4.3.1 Terminology

When a user logs in, a new session is created, which consists of a new process group, comprising a single process that is running the login shell. That process is the process-group leader, and its process ID (73056, say) is the process-group ID. That process is also the session leader, and the process ID is also the session ID.^5 The terminal from which the user logged in becomes the controlling terminal of the session. The session leader is also the controlling process. This arrangement is shown in the right part of Figure 4.1, with the process group marked FG, for foreground.

![](img/41b4c8f6d6a5c349eee321a301703d97_238_0.png)

*process-group leader †session leader*

**Figure 4.1** Session, process groups, processes, and controlling terminal.

> 5. The various standards use the phrase “process-group ID of the session leader,” but I prefer to just call it the session ID.

If *job control* is enabled by the shell and a command or pipeline of commands is then run in the background, like this:

```bash
$ du -a | grep tmp >out.tmp
```

a new process group is formed, this time with two processes in it, as shown at the left of Figure 4.1, with the process group marked BG, for background. One of the two new processes is the leader of this new process group.

Both process groups (73056 and 73381) are in the same session and have the same controlling terminal. With job control, a new process group is created for each command line, and each such process group is also called a *job*.

Just because a process group runs in the background, it doesn’t mean its standard file descriptors aren’t still directed to and from the terminal. In the previous example pipeline, du’s standard output is connected via a pipe to the standard input of grep, and grep’s standard output is redirected to a file, but that’s because the user specifically set them up that way, not because they’re running in the background.

What job control does mean is that if certain signals are generated from the controlling terminal, such as *interrupt* (*SIGINT*), *quit* (*SIGQUIT*), or *suspend* (*SIGSTP*), they are only sent to the foreground process group, leaving any background process groups alone. The “control” part means that the user can execute shell commands to move process groups (jobs) back and forth between foreground and background. Usually, if a process group is running in the foreground, a Ctrl-z sends it a *SIGSTP* signal, which causes the shell to move it to the background, bringing one of the background process groups to the foreground. Or the fg shell command can bring a specific background process group to the foreground, which also then sends the old foreground process group to the background.

If job control is not enabled, the two new processes in the example pipeline (running du and grep) don’t run in their own process group, but run in process group 73056, along with the first process, the shell, as shown in Figure 4.2. They still run in the background, but all that means is that the shell doesn’t wait for them to complete. As there is only one process group, there is no way to move process groups between foreground and background, and any signals generated from the controlling terminal go to all processes in the only process group in the session. Typing Ctrl-c at the terminal will send a *SIGINT* to all three processes, including the two background processes, and, unless those processes have set themselves up to catch or ignore the signal, it will terminate them, which is the default action for this particular signal. (Much more about signals in Chapter 9.)

![](img/41b4c8f6d6a5c349eee321a301703d97_240_0.png)

**Figure 4.2** No job control; only one process group per session.

With or without job control, when the controlling terminal hangs up or is disconnected, a SIGHUP signal is sent to the controlling process, and the default for that signal is to terminate it. For a typical session, this terminates the login shell and logs out the user. The controlling terminal is no longer the controlling terminal for the session, which then has no controlling terminal. Whether other processes in the session can continue to access the terminal is not specified by any of the standards, and most implementations will probably prevent such access by, for example, returning an error from a read or write.

However, once the controlling process terminates for any reason (not just receiving a SIGHUP), every process in the foreground (or only) process group gets a SIGHUP, which by default causes them to terminate. Unless they've arranged to catch or ignore this signal, they never get far enough to attempt to access the former controlling terminal.

What happens if a process in a background process group attempts to access the controlling terminal? Regardless of whether the controlling process is running, the basic rule is that any attempt by a background process to read the controlling terminal causes it to be sent a SIGTTIN signal, and any attempt to write it generates a SIGTTOU signal. Here “write” also means using the terminal-control system calls tcsetattr, tcdrain, tcflow, tcflush, and tcsendbreak (Sections 4.5 and 4.6).

The default behavior for these signals is to suspend the process, which makes a lot of sense: Background processes that need access to the controlling terminal stop, and you move them to the foreground when you're ready to interact with them.

The exceptions to the basic rule are:

- A background process attempting to read with `SIGTTIN` signals ignored or blocked instead gets an `EIO` error from `read`.
- An orphaned background process (process-group leader has terminated) also gets an `EIO` from `read`.
- If the `TOSTOP` terminal attribute (see Section 4.5.6) is clear, the process is allowed to write.
- If `TOSTOP` is set but `SIGTTOU` signals are ignored or blocked, the process is allowed to write.
- If `TOSTOP` is set, an orphaned background process gets an `EIO` error from `write`.

So, to summarize the rules: A background process can't read the controlling terminal no matter what; it gets an error or is stopped. An orphaned background process gets an error if it tries to write the terminal. Nonorphaned background processes can write it if `TOSTOP` is clear or if `SIGTTOU` are ignored or blocked; otherwise they are stopped.

The asymmetry between reading and writing is because it never makes sense for two processes to both read characters—it's much too dangerous. (Imagine typing `rm *.o` and having the shell only get `rm *.`.) Two processes writing is only confusing, and if that's what the user really wants, then so be it.

### 4.3.2 System Calls for Sessions

**setsid**--create session and process group

```c
#include <unistd.h>

pid_t setsid(void);
/* Returns process-group ID or -1 on error (sets errno) */
```

**getsid**--get session ID

```c
#include <unistd.h>

pid_t getsid(
    pid_t pid               /* process ID or 0 for calling process */
);
/* Returns session ID or -1 on error (sets errno) */
```
