
```c
void sig_handler(int signal) {
    fprintf(stderr, "pid %d received signal %d\n",
           getpid(), signal);
    child_restart_children = 0;

    #if 0
        /* wake up the wait() */
        /* doesn't work * */
        raise(SIGCHLD);
    #endif

    longjmp(jump_env, 1);
}

/* We opt not to call signal() again here */
/* next signal may kill us * */

main() {
    int i;
    int child;
    child_group_info_t child_group_1;
    child_groups_t child_groups;
    int rc;

    #if 0
        setvbuf(stderr, NULL, _IOLBF, 0);
    #else
        setvbuf(stderr, NULL);
    #endif

    /* Note: children inherit this * */
    signal(SIGTERM, sig_handler);
    signal(SIGINT, sig_handler);
    signal(SIGQUIT, sig_handler);

    child_group_create(&child_group_1, 4, 4, child_process_1, NULL);

    child_groups.ngroups = 1;
    child_groups.group[0] = &child_group_1;

    rc = setjmp(jump_env);
    if (rc == 0) {
        child_groups_keepalive(&child_groups);
    } else {
        /* exception handler */
        /* we got here via setjmp() */

        /* restore signal handlers to defaults */
        signal(SIGTERM, SIG_DFL);
        signal(SIGINT, SIG_DFL);
        signal(SIGQUIT, SIG_DFL);

        child_groups_kill(&child_groups);
        exit(0);
    }
}
```

# The child_demo2.c Program

The `child_demo2.c`, shown in `Listing 11.4`, is an extension of `child_demo1.c`. It implements a primitive Web server, which preforks 4 processes, each of which responds to any request by reporting the status of the child process that handled the request. Each request will terminate after it has handled 10 requests. In a prefork server situation, you may need to guard against memory leaks and other problems by giving each child a limited lifetime. It would also be good to set an alarm at the beginning of each request so the child will die if the request is not handled in a reasonable time for any reason.

# Listing 11.4 child_demo2.c
