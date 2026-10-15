
```c
int main(int argc, char* argv[])
{
    pid_t      pid;
    siginfo_t  siginfo;

    if ( -1 == (pid = fork())) {
        perror("fork");
        exit(1);
    }
    else if ( 0 == pid ) {
        printf("Child pid is %d\n", getpid());
        sleep(SLEEPTIME);
        exit(0);
    }
    /* Parent code */
    else do {
        /* Zero out si_pid in case the siginfo_t struct does not get */
        /* initialized because no children are waitable. */
        siginfo.si_pid = 0;

        /* Wait for changes in the state of the child created above, */
        /* specifically, stopping, resuming, exiting, and return */
        /* immediately if no child is waitable. */
        if (-1 == waitid(P_PID, pid, &siginfo,
            WEXITED | WSTOPPED | WCONTINUED | WNOHANG) ) {
            perror("waitid");
            exit(EXIT_FAILURE);
        }
        if ( siginfo.si_pid == 0 )
            /* no child is waitable. */
            continue;
        switch ( siginfo.si_code ) {
            case CLD_EXITED:
                printf("Child exited with status %d\n",
                    siginfo.si_status );
                break;
            case CLD_KILLED:
            case CLD_DUMPED:
                printf("Child killed by signal %d\n",
                    siginfo.si_status );
                break;
            case CLD_STOPPED:
                printf("Child stopped by signal %d\n",
                    siginfo.si_status );
                break;
            case CLD_CONTINUED:
                printf("Child continued\n");
                break;
        }
    } while ( siginfo.si_code != CLD_EXITED &&
             siginfo.si_code != CLD_KILLED &&
             siginfo.si_code != CLD_DUMPED );
    return 0;
}
```

## Notes.

- The si_status field does not need to be bit-manipulated to extract its value. The value contained there has already been shifted as necessary.
- The while-loop in the parent continues until the child is killed or terminated to give you a chance to stop and continue the child.
- If you run this program in one terminal, and then from another issue kill commands, or run it in the background on one terminal and issue kill commands on the same terminal, you will see output like the following:

```
$ waitiddemo 77
Child pid is 15243
Child exited with status 77
$
```

Then do it again without the command-line argument:

```
$ waitiddemo &
Child pid is 15245
$ kill -STOP 15245
Child stopped by signal 19
$ kill -CONT 15245
Child continued
$ kill -TERM 15245
Child killed by signal 15
[1]+ Done waitiddemo
$
```

## 7.10 Summary

The four principal tools in process creation and control are fork(), exec(), exit(), and wait() and their related functions. Add to the toolbox the things you have learned about signals and signal handling and you have the means of creating and managing processes effectively. What is still lacking is a means for these processes to exchange and share data effectively. At this point the only way they can share data other than provided by the signal mechanism is through the file system, which is extremely slow. Inter-process communication is the topic of the next chapter.

Because the new process is a copy of the parent process, it shares all open files and all library buffers. When the two processes both use the C I/O Library, care must be taken to prevent unexpected consequences of this.

Process creation is a time-consuming activity in the kernel, with high overhead in memory copying. When the objective is to use shared variables and common code, light-weight processes, or threads, are the better solution. This topic follows as well.

## Bibliography

[1] Keith Haviland, Marcus Gray, and Ben Salama. *Unix System Programming*. Addison-Wesley Longman, Inc., 2nd edition, 1998.

## Chapter 8 Interprocess Communication, Part I

## Concepts Covered

- *Pipes*
- *I/O Redirection*
- *FIFOs*
- *Concurrent Servers*
- *Daemons*
- *Multiplexed I/O with select()*
- *API: dup, dup2, fpathconf, mkfifo, mknod, pipe, pclose, popen, select, setsid, shutdown, syslog, tee.*

## 8.1 Introduction

Processes that cooperate in order to complete one or more tasks almost always need to communicate with each other. Sometimes the communication requires sharing data. One method of sharing data is by sharing a common file. If at least one of the processes modifies the file, then the file must be accessed in mutual exclusion. Sharing a file is essentially like sharing a memory-resident resource in that both are a form of communication that uses a shared resource that is accessed in mutual exclusion. Another paradigm involves passing data back and forth through some type of communication channel that provides the required mutual exclusion. A pipe is an example of this, as is a socket. This type of communication is broadly known as a *message-passing* solution to the problem.

This chapter is concerned only with message-passing types of communication. We will begin with *unnamed pipes*, after which we will look at *named pipes*, also known as *FIFO’s*, and then look at *sockets*. Part I is exclusively related to pipes.

## 8.2 Unnamed Pipes

You are familiar with how to use pipes at the command level. A command such as

```
$ last | grep 'reboot'
```

connects the output of *last* to the input of *grep*, so that the only lines of output will be those lines of *last* that contain the word ‘reboot’. The ‘|’ is a *bash* operator; it causes *bash* to start the *last* command and the *grep* command *simultaneously*, and to direct the standard output of *last* into the standard input of *grep*.

Although ‘|’ is a *bash* operator, it uses the lower-level, underlying *pipe* facility of UNIX, which was invented by Douglas McIlroy, and was incorporated into UNIX in 1973. You can visualize the pipe mechanism as a special file or buffer that acts quite literally like a physical pipe, connecting the output of *last* to the input of *grep*, as in Figure 8.1.

The *last* program does not know that it is writing to a pipe and *grep* does not know that it is reading from a pipe. Moreover, if *last* tries to write to the pipe faster than *grep* can drain it, *last*
