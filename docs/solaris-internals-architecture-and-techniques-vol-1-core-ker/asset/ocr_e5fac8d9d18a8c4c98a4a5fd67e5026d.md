# System Calls

(sy_lock) for loadable system calls. The system call itself is referenced through a function pointer: sy_call or sy_callc.

> Historical Aside: The fact that there are two entries for the system call functions is the result of a rewriting of the system argument-passing implementation, an effort that first appeared in Solaris 2.4. Earlier Solaris versions passed system call arguments in the traditional UNIX way: bundling the arguments into a structure and passing the structure pointer (uap is the historical name in UNIX implementations and texts; it refers to a user pointer). Most of the system calls in Solaris have been rewritten to use the C language argument-passing convention implemented for function calls. Using that convention provided better overall system call performance because the code can take advantage of the argument-passing features inherent in the register window implementation of SPARC processors (using the in registers for argument passing—refer to [31] for a description of SPARC register windows).

sy_call represents an entry for system calls and uses the older uap pointer version, maintained for binary compatibility with older versions of Solaris. sy_call is the function pointer for the most recent argument-passing implementation. The newer C style argument passing has shown significant overall performance improvements in system call execution—on the order of 30 percent in some cases.

```
main() {
    int fd;
    int bytes;
    fd=open("file", O_RDWR);
    if (fd == -1) {
        perror("open");
        exit(-1);
    } else {
        bytes=read(fd,buf, ...);
    }
}
```

![](bbox=[0.125, 0.555, 0.902, 0.915])

Figure 2.9 System Call Execution