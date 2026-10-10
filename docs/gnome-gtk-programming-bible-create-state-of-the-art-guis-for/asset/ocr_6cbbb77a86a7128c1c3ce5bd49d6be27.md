# Executing a Command Line

Using the function `system()`, you can enter the same kind of commands from inside a program that you can enter from the command line. The following example demonstrates the sort of things that you can do:

```
/* system.c */
#include <unistd.h>

int main(int argc, char *argv[]) {
    int pid1;
    int pid2;

    pid1 = system("grep print *.c\n");
    pid2 = system("grep include *.c >inclist &\n");
    wait(pid2);
    exit(0);
}
```

A `system()` function call executes a fork and exec to get a command shell that runs the command. The first one instructs `grep` to run in the foreground and display its results to the standard output, as it normally does. The second `system()` call both redirects the output and, by including an ampersand, runs the command as a child process. The call to `system()` waits until the command completes, unless it is run as a child process.

A return value of -1 indicates there is an error with the command passed to it. A return value of 127 indicates that the command line shell could not be started. If there are no errors, and the command is not being run in the background, the value resulting from the execution of the command is returned. If, however, the program is run in the background (as in the second `system()` call in the example), the process ID of the child is returned and you need to call `wait()` just as with fork and exec.

> There is something a bit odd about the return value from `system()`. It has an error return code of 127. A valid return value from a command also can be 127. If this poses a problem, use fork and exec.

# Pipes

A *pipe* is a one-way connection between a pair of processes. The function `popen()` spawns a child process and creates a pipe connected to it. Depending on the direction of the pipe, the child process either can read from it by reading its own standard input or write to it by writing to its own standard output. For