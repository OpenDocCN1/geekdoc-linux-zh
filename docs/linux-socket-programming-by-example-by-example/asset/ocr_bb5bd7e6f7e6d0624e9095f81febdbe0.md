```
27:        return 1;            /* Failed */
28:    }
29:
30:    /*
31:     * Report the socket file descriptors returned:
32:     */
33:    printf("s[0] = %d\n", s[0]);
34:    printf("s[1] = %d\n", s[1]);
35:
36:    system("netstat --unix -p");
37:
38:    return 0;
39: }
```

# NOTE

If you have an older version of Linux (pre Red Hat 6.0) the netstat command used in line 36 of Listing 1.1 may not understand the options used.

If this is the case, you may want to try changing line 36 to read:

```
system("lsof -i tcp");
```

This requires that lsof is installed on your system. lsof command may be obtained from a variety of sources. A good place to start is

ftp://vio.cc.purdue.edu/pub/tools/unix/lsof/

Various mirror sites are listed there, in addition to the source code. Note also that when using lsof, you may need to execute the program in Listing 1.1 as root.

lsof may also be found in binary (including RPM) and source formats under the various distribution directories under

ftp://sunsite.unc.edu/pub/Linux/distributions

As a last resort, you may substitute the following statement for line 36:

```
system("netstat | grep tcp");
```

The demonstration program can be described in the following steps:

+   1.  A receiving array s[2] is declared in line 16 to receive the two new file descriptors that will reference the two new sockets being created.

+   2.  The socketpair(2) function is invoked in line 21. The domain argument is specified as AF \_ LOCAL, the socket type argument is SOCK \_ STREAM and the protocol is specified as zero.

+   3.  The if statement in line 23 tests to see if the socketpair(2) function was successful. If z contains a value of -1, the failure is reported to standard error (lines 24 to 26) and the program exits in line 27.