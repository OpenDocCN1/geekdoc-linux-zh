```
```c
                uts.machine);
            printf("                 Node name: %s\n",
                uts.nodename);
    #ifdef USE_GNU
            printf("                 Domain name: %s\n",
                uts.domainname);
    #else
            printf("                 Domain name: %s\n",
                uts.__domainname);
    #endif

        if(getcwd(cwd,sizeof(cwd)))
            printf("                 Current directory: %s\n",
                cwd);

        if((env = getenv("SHELL")) != NULL)
            printf("                 Environment variable SHELL: %s\n",
                env);
        printf("                 User ID: %ld\n",
            (long) getuid());
        printf("                 Group ID: %ld\n",
            (long) getgid());
        printf("                 Process ID: %ld\n",
            (long) getpid());
        printf("                 Login: %s\n",
            (long) getppid());
        printf("                 User shell: %s\n",
            getusershell());
        printf("Maximum arg length for exec(): %ld\n",
            sysconf(_SC_ARG_MAX));
        printf("    Maximum processes per user: %ld\n",
            sysconf(_SC_CHILD_MAX));
        printf("    Clock ticks per second: %ld\n",
            sysconf(_SC_CLK_TCK));
        printf("    Maximum streams per process: %ld\n",
            sysconf(_SC_STREAM_MAX));
        printf("Maximum open files per process: %ld\n",
            sysconf(_SC_OPEN_MAX));
        printf("Maximum chars in timezone name: %ld\n",
            sysconf(_SC_TZNAME_MAX));
        printf("    Maximum command line length: %ld\n",
            sysconf(_SC_LINE_MAX));
        printf("    POSIX job control supported: %s\n",
            sysconf(_SC_CHILD_MAX)? "true" : "false");
        printf("    POSIX.1 compliance (YYYYMM): %ld\n",
            sysconf(_SC_VERSION));
        printf("    POSIX.2 compliance (YYYYMM): %ld\n",
            sysconf(_SC_2_VERSION));
        printf("    POSIX.2 Locale by localdef: %s\n",
            sysconf(_SC_2_LOCALEDEF)? "true" : "false");
        printf("    POSIX.2 software development: %s\n",
```
```