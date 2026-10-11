> NOTE  Only the least-significant eight bits of the value are available to the parent process. Thus, you should use values in the range 0–255. As we’ll see shortly, 126 and 127 have a conventional meaning (above and beyond plain “unsuccessful”), to which your programs should adhere.
> 
> Since only the least-significant eight bits matter, you should never use a negative exit status. When the last eight bits are retrieved from small negative numbers, they become large positive values! (For example, –1 becomes 255, and –5 becomes 251.) We have seen C programming books that get this wrong—don’t be misled.

# 9.1.5.2 Returning from main()

A program can terminate voluntarily in one of two ways: by using one of the functions described next or by returning from main(). (A third, more drastic, way, is described later, in Section 12.4, “Committing Suicide: abort(),” page 445.) In the latter case, you should use an explicit return value instead of falling off the end of the function:

```
/* Good: */
int main(int argc, char * * argv)
{
    /* code here */
    return 0;
}

/* Bad: */
int main(int argc, char * * argv)
{
    /* code here */
    /* ?? What does main() return ?? */
}
```

The 1999 C standard indicates that when main() returns by falling off the end, the behavior is as if it had returned 0. (This is also true for C++; however, the 1989 C standard leaves this case purposely undefined.) In all cases, it’s poor practice to rely on this behavior; one day you may be programming for a system with meager C runtime support or an embedded system, or somewhere else where it will make a difference. (In general, falling off the end of any non-void function is a bad idea; it can only lead to buggy code.)

The value returned from main() is automatically passed back to the system, from which the parent can recover it later. We describe how in Section 9.1.6.1, “Using POSIX Functions: wait() and waitpid(),” page 306.

> NOTE On GNU/Linux systems, the gcc compiler-driver command runs the compiler with the appropriate options such that the return value when falling off the end is 0. Plain gcc doesn’t do this.