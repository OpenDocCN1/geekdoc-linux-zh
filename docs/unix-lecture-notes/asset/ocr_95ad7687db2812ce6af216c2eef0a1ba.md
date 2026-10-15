group leaders can do this. Since the server is now a child of the original process, it is neither, so it can call setsid(), which makes it a session leader of a new session and a group leader of a new process group.

+   3. Registering its intent to ignore SIGHUP.

+   4. Forking another child process, terminating in the parent again, and letting the new child, which is the grandchild of the original process, execute the server code. In some versions of UNIX, when a session leader opens a terminal device (which it may want to do sometimes), that terminal is automatically made the control terminal for the process. By running as the child of a session leader, the server is now immune from this eventuality. In Linux, a process can set the O_NOCTTY flag on open() to prevent this. The reason for ignoring SIGHUP is that when a session leader terminates, all of its children are sent a SIGHUP, which would otherwise kill them. Since the parent is a session leader, the child must ignore SIGHUP.

+   5. Changing the working directory to "/".

+   6. Clearing the umask.

+   7. Closing any open file descriptors.

A procedure for doing all of these steps, based on one from [Stevens], is below.

# Listing 8.17: daemon_init.c

```
void daemon_init(const char *pname, int facility)
{
    int     i;
    pid_t   pid;

    if ( (pid = fork()) == -1) {
        perror("fork");
        exit(1);
    }
    else if (pid != 0)
        exit(0);            /* parent terminates */

    /* Child continues from here */
    /* Detach itself and make itself a session leader */
    setsid();

    /* Ignore SIGHUP */
    signal(SIGHUP, SIG_IGN);

    if ( (pid = fork()) == -1) {
        perror("fork");
        exit(1);
    }
    else if ( pid != 0 )
        exit(0);    /* First child terminates */

    /* Grandchild continues from here */
    chdir("/");         /* change working directory */
```