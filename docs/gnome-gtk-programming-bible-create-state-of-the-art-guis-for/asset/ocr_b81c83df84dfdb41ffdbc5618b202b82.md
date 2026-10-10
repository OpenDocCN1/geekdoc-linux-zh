Line 18 is a call to a function named `wait()`. This function blocks and does not return until a child process dies. If you have no child processes, it returns immediately. If you have more than one child process, you have to call `wait()` for each one of them. There are a number of approaches you can take to wait for child processes to die, but you do need to acknowledge them with some form of the `wait()` function call. This is because every process continues to exist until it reports its status to its parent process. If you are in a situation in which you are spawning a lot of child processes, you need to set up some procedure by which you check for child processes that die. There are four functions designed to wait in different ways and return different values—you can see them by entering `man wait` and `man wait3`. The status value returned by these functions contains the return code from the program, along with some flags that explain how the child died.

The following program is spawned by the fork and exec:

```


```c
/* showargs */
int main(int argc, char *argv[])
{
    int i;

    for (i=0; i<argc; i++)
        printf(" %d %s\n", i, argv[i]);
    return(66);
}
```
```

All this program does is display each of the arguments found on the command line. The output can look like this:

```


Parent: pid=23018 childpid=23019
Child: pid=23019 parentpid=23018
0 first
1 second
2 third
Parent: child 23019 died
```

Immediately following the fork, the parent process displays its process ID, and the ID of the child, and calls `wait()` to detect child termination. Simultaneously, the child process is displaying its information and forking to another process that also displays some strings. The order of the statements shown may vary because the two processes are asynchronous—for example, if the child is faster than the parent, both of the parent’s display lines may appear at the bottom.

> > **Note**
> >
> > The first argument passed to `showargs` is not, as you might expect, the name of the program. It is the first argument string you passed to the `exec1p()` function. To correct this, you can pass the name of the program or you can use one of the other `exec()` functions.