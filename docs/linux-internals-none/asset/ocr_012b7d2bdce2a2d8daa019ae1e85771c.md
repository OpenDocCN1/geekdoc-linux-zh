```
static int init(void * unused)
{
    lock_kernel();
    do_basic_setup();

    /*
     * Ok, we have completed the initial bootup, and
     * we're essentially up and running. Get rid of the
     * initmem segments and start the user-mode stuff..
     */
    free_initmem();
    unlock_kernel();

    if (open("/dev/console", O_RDWR, 0) < 0)
        printk("Warning: unable to open an initial console.\n");

    (void) dup(0);
    (void) dup(0);

    /*
     * We try each of these until one succeeds.
     *
     * The Bourne shell can be used instead of init if we are
     * trying to recover a really broken machine.
     */
    if (execute_command)
        execve(execute_command,argv_init,envp_init);
    execve("/sbin/init",argv_init,envp_init);
    execve("/etc/init",argv_init,envp_init);
    execve("/bin/init",argv_init,envp_init);
    execve("/bin/sh",argv_init,envp_init);
    panic("No init found.  Try passing init= option to kernel.");
}

```

Here, init is entered as a kernel task and goes to create a user space process called, unsurprisingly, init. The init function is declared unused because it is not passed any arguments; it just reads the code for the user space program from disk and launches it.

Init is always assigned the process ID (PID) number 1. Why not 0, as counting is usually done in the computer industry? Because 0 is already taken by the idle process that is created at boot time.

In the above code, you can also see from where the console message indicating that some memory has been freed during boot comes: free_initmem. This function releases the no longer needed function in the .text.init section of the kernel. This is a typical message generated on a 512MB RAM system (here named hatta) at boot:

```
Mar 19 09:14:35 hatta kernel: Freeing unused kernel memory: 72k freed
```