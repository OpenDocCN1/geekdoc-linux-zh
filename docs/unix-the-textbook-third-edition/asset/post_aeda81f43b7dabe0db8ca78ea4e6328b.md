
## TABLE 21.4 Web Resources for Practical Consideration in Server Design

| https://www.freebsd.org/ | Home page for FreeBSD. Contains a lot of useful material, including FreeBSD source, manual pages, support, SVN repository, forums, user groups, etc. |
| https://www.freebsd.org/doc/handbook/ | The page for FreeBSD documentation. An excellent resource for anything you want to know about FreeBSD |
| https://www.netbsd.org/docs/guide/en/chap-inetd.html | An excellent page on the UNIX superserver, inetd |
| https://www.freebsd.org/doc/handbook/network-inetd.html | Another excellent page on the UNIX superserver, inetd |

We then discussed the various issues important for the design of a production server. These issues are: creating a daemon, setting signals and umask, ensuring that only a single copy of a process may run at a given time, saving the PID of the daemon at a known place, detaching the terminal from the daemon, changing the working directory, closing inherited standard descriptors, and opening standard descriptors and attaching them to a benign device; finally, we presented a simple server that has all of these features. Along the way, we discussed two methods of file locking using the flock() and fcntl() system calls. At the end, we outlined the steps necessary for the creation of a concurrent, connection-oriented production server that uses slave processes to serve clients.

Throughout the chapter, we showed the uses of the various system calls and library functions in small C code fragments and programs to illustrate different issues related to the design of UNIX servers. Finally, we combined all the code fragments to get the final version of a server that runs on both Solaris and PC-BSD systems. In order to make the code portable across all UNIX systems, remove the conditional compilation and only compile the file-locking code based on fcntl().

## QUESTIONS AND PROBLEMS

- 1. When does the issue of restarting a system call arise?
- 2. What is a thread-safe system call? What are the issues that make a system call not thread safe.
- 3. What is reentrant code? Why is this property important in a program? Give examples of a few common applications or tools that are reentrant.
- 4. What are the implications of reentrant code from the point of view of memory management on a time-sharing system? Give a small example to illustrate your answer.
- 5. Which of the following functions are thread safe and/or reentrant? Explain your answers.

```
a. int test;
void swap(int *first, int *b)
{
    test = *first;
    *first = *b;
    *b = test;
}
```

```
b. int test;
void swap(int *first, int *b)
{
    int q;
    q = test;
    test = *first;
    *first = *b;
    *b = test;
    test = q;
}
```

```
c. int sec_var = 1;
int first()
{
    sec_var = sec_var + 2;
    return sec_var;
}
```

```
d. int sec()
{
    return first() + 2;
}
```

```
e. int first(int i)
{
    return i + 2;
}
```

```
f. int sec(int i)
{
    return first(i) + 2;
}
```

- 6. What is a daemon? Name five daemons in a typical UNIX system. Write down the purpose of each.
- 7. Why should a server close all inherited descriptors?
- 8. Why does a server process open the standard descriptors after closing all inherited descriptors? Why are the newly opened standard descriptors attached to a device like /dev/null?
- 9. What kind of locks can be placed on a file using the flock() system call? What is the purpose of each lock?
- 10. Suppose a process has locked a file ABC for exclusive access using the flock() system call. The process forks a child and the child unlocks the file. Will the parent still have exclusive access to file? Explain your answer.
- 11. Why should a daemon be coded such that only one instance of it may execute at any given time? What is the most common method of doing so? Write a small server program in C that uses this method. Compile and run the program, and show that your method works.
- 12. Consider the code shown in Section 21.7 for locking a file for mutually exclusive access by a process. Change

```
#define LOCKFILE "/usr/home/sarwar/Servers/testd.lock"
```

to

```
#define LOCKFILE "./Servers/testd.lock"
```
