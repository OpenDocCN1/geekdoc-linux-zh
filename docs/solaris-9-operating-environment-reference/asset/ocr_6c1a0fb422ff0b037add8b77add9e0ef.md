# apptrace 53

```
return = (gid_t) 10 (0xa)
id -> libc.so.1:getgrid(gid = 0xa) = 0x2325c
gid = (gid_t) 10 (0xa)
return = (struct group*) 0x2325c (struct group) (
gr_name: (char*) 0x23270 "staff"
gr_password: (char *) 0x23276 **
gr_gid: (gid_t) 10 (0xa)
gr_mem: (char **) 0x2325c
}

id -> libc.so.1:getgrid(gid = 0xa) = 0x2325c
gid = (gid_t) 10 (0xa)
return = (struct group*) 0x2325c (struct group) (
gr_name: (char*) 0x23270 "staff"
gr_password: (char *) 0x23276 **
gr_gid: (gid_t) 10 (0xa)
gr_mem: (char **) 0x2325c
}
```

uid=1001(winsor) gid=10(staff) groups=10 (staff)
mopoke()

# Files

To perform printing of arguments when tracing calls (selected as the -v option), apptrace needs to know the name and data types of the arguments supplied to the called interface, apptrace relies on special runtime support shared objects for formatted printing. A runtime support object is provided for each Solaris library which contains an interceptor function for each interface within the shared library; these supporting objects are stored in the libabi directory. A simple example allows to map the name of a library interface to an interceptor function in the library's object that supports verbose-tracing. Apptrace does not find an interceptor in the library's board that supports tracing, apptrace cannot determine the name or data types of the arguments for interface, apptrace uses a default output for the call-tracing report (hex-formatted printing of the first three arguments).

# Limitations

In general, apptrace cannot trace calls to functions accepting variable argument lists. Some clever coding works around this limitation, most notably in the printf function.

Functions that try to probe the stack or extract information about the caller cannot be traced. Some examples are [siggetcontext(), getspinfo(), siglongjmp(), [sigsetcontext()], and fork().

Functions such as do not return can also produce strange output. Also, functions that called functions produce before returning slightly gathered output.

For security reasons, only root can run apptrace on setuid/setgid programs. Tracing functions, such as fprintf(3XURSES) and vsprintf(3XURSES), whose requires the inclusion of varargs.h, do not provide formatted printing of