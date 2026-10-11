+   • sigprocmask Sets or modifies the list of signals that a process wants to block

# System Call Return Codes

System calls almost always return 0 when they succeed and return a negative number (almost always -1) when an error occurred, so there are (at least) two ways to check the return value.

# Examples

![](bbox=[0.05, 0.23, 0.11, 0.28])

# Example

+   1. This code snippet compares a system call return code to 0.

```
if(open("/usr/src/linux/Makefile", O_RDONLY)) {
    /* an error occurred, handle it here */
} else {
    /* open the file successfully */
}
```

This example uses the fact that successful system calls return 0. The if condition will test true if the open call fails, so the appropriate error handling code will execute.

+   2. This snippet specifically evaluates whether the system call returns a negative value and acts appropriately.

![](bbox=[0.05, 0.53, 0.11, 0.57])

# Example

```
if(open("/usr/src/linux/Makefile", O_RDONLY) < 0) {
    /* an error occurred, handle it here */
} else {
    /* opened the file successfully */
}
```

The second example explicitly tests for a negative return value from open. Other than the different if conditions, the two examples behave precisely the same way. The first one is a common C idiom, so you will encounter it a great deal. I prefer the second example because it is easier for novices to understand, but the choice is yours (this is Linux, after all).

# Table of System Call Error Codes

Table 6.1 contains an annotated list of the errors that system calls generally return. Because you are still learning to program in the Linux environment, you probably will not understand a lot of these errors. Read through the list to get a general idea, and then, as you read the rest of this book and work through the example programs, review the list.

The manual page for each system call documents all of the error codes it generates. In addition, all of the error codes defined by POSIX, the