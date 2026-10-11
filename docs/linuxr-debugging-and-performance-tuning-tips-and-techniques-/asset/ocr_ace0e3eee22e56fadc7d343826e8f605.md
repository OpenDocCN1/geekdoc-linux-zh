Pure BSD systems (4.3 Reno and later) support all of the fields. Table 9.2 describes the availability of the various fields in the struct rusage for POSIX and Linux.

# TABLE 9.2
Availability of struct rusage fields

| Field | POSIX | Linux | Field | POSIX | Linux |
| :--- | :--- | :--- | :--- | :--- | :--- |
| ru_utime | ✓ | \geq 2.4 | ru_nswap | | \geq 2.4 |
| ru_stime | ✓ | \geq 2.4 | ru_nvcsw | | \geq 2.6 |
| ru_minflt | | \geq 2.4 | ru_nivcsw | | \geq 2.6 |
| ru_majflt | | \geq 2.4 | | | |

Only the fields marked “POSIX” are defined by the standard. While Linux defines the full structure, the 2.4 kernel maintains only the user-time and system-time fields. The 2.6 kernel also maintains the fields related to context switching.³

The fields of most interest are ru_utime and ru_stime, the user and system CPU times, respectively. (User CPU time is time spent executing user-level code. System CPU time is time spent in the kernel on behalf of the process.)

These two fields use a struct timeval, which maintains time values down to microsecond intervals. See Section 14.3.1, “Microsecond Times: gettimeofday(),” page 544, for more information on this structure.

In 4.2 and 4.3 BSD, the status argument to wait() and wait3() was a union wait. It fit into an int and provided access to the same information as the modern WIFEXITED() etc. macros do, but through the union’s members. Not all members were valid in all situations. The members and their uses are described in Table 9.3.

POSIX doesn’t standardize the union wait, and 4.4 BSD doesn’t document it, instead using the POSIX macros. GLIBC jumps through several hoops to make old code using it continue to work. We describe it here primarily so that you’ll recognize it if you see it; new code should use the macros described in Section 9.1.6.1, “Using POSIX Functions: wait() and waitpid(),” page 306.