The killer.c program in the following session takes a PID and a signal number as command line arguments and uses the kill() system call to send the specified signal to the process with the given PID. After compiling the program and saving the executable code in the file called killer, we start a C shell process, and use the ps command to see the PID of the new C shell process. We then use the killer program to send signal number 2 (SIGINT) to the new C shell process (PID 53426). The output of the ps command shows that, as expected, the C shell does not terminate. When we send signal number 9 (SIGKILL; sure kill) to the new C shell process, the shell terminates. The SIGHUP signal would also terminate the shell process.

```
% cat killer.c
/* killer.c: killer signal pid */
#include <sys/types.h>
int main(int argc, char *argv[])
{
    pid_t pid;
    int signal;
    if (argc != 3) {
        printf("Inappropriate number of command line arguments.\n");
        exit(0);
    }
    pid = atoi(argv[1]);
    signal = atoi(argv[2]);
    if (kill(pid, signal) == -1) {
        perror("Kill failed");
        exit(1);
    }
    exit(0);
}
```

```
% gcc48 -w killer.c -o killer
% csh
% ps
PID TT STAT TIME COMMAND
51926 1 Ss 0:00.29 -csh (csh)
53426 1 S 0:00.28 csh
53435 1 R+ 0:00.00 ps
% ./killer 53426 2
% ps
PID TT STAT TIME COMMAND
51926 1 Ss 0:00.29 -csh (csh)
53426 1 S 0:00.28 csh
53435 1 R+ 0:00.00 ps
% ./killer 53426 9
```