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

6. What is a daemon? Name five daemons in a typical UNIX system. Write down the purpose of each.

7. Why should a server close all inherited descriptors?

8. Why does a server process open the standard descriptors after closing all inherited descriptors? Why are the newly opened standard descriptors attached to a device like /dev/null?

9. What kind of locks can be placed on a file using the flock() system call? What is the purpose of each lock?

10. Suppose a process has locked a file ABC for exclusive access using the flock() system call. The process forks a child and the child unlocks the file. Will the parent still have exclusive access to file? Explain your answer.

11. Why should a daemon be coded such that only one instance of it may execute at any given time? What is the most common method of doing so? Write a small server program in C that uses this method. Compile and run the program, and show that your method works.

12. Consider the code shown in Section 21.7 for locking a file for mutually exclusive access by a process. Change

```
#define LOCKFILE "/usr/home/sarwar/Servers/testd.lock"
```

to

```
#define LOCKFILE "./Servers/testd.lock"
```