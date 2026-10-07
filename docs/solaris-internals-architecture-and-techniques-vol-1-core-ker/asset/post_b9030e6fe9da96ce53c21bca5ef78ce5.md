
# Solaris Files and File I/O

cated device driver-level support yield overall faster and more efficient I/O operations. On relatively small, lightly loaded systems, the improvement is less dramatic, with typical performance improvements on the order of 5 to 6 percent. As the size of the system (number of processors and amount of RAM) increases and the number of async I/O requests (load) grows, the kaio approach delivers much more scalable performance, with improvements measuring up to 30 percent over some benchmarks. Your mileage will, of course.

Kaio is implemented as a loadable kernel module, /kernel/sys/kaio, and is loaded the first time an async I/O is called. You can determine if the module is loaded with modinfo(IM).

```
$ modinfo | grep kaio
105 608c4000 2efd178 1 kaio (kernel Async I/O)
```

If the preceding command returns nothing, it simply means the kaio kernel hasn't been loaded. The system loads automatically as needed.

There's a relatively simple test you can run to determine whether or not you have kaio support available for a given file. It involves compiling and running a small program that calls airead(3) and uses truss(1) on the program to watch the system-call activity. First, here's the C language source code.

```
* Quick kaio test. Read lk bytes from a file using async I/O.
* To compile:
* cc -o aio.c -laio
* To run:
* aio file_name
 *
#include <sys/stdio.h>
#include <sys/types.h>
#include <sys/fcntl.h>
#include <sys/aio.h>

#define BSIZE 1024

main(int argc, char *argv[])
{
    aio_result t res;
    char buf[BSIZE];
    int fd;

    if ((fd = open(argv[1], O_RDONLY)) == -1) {
        perror("open");
        exit(-1);
    }

    airead(fd, buf, BSIZE, 0, SEEK_SET, &res);
    aitwait(0);
    if (res.aio_return == BSIZE) {
        printf("aio succeeded\n");
        close(fd);
        exit(0);
    }
    perror("aio");
}
```

# Asynchronous I/O

Once you have the test program compiled, use the truss(1) command to do a system-call trace of the execution path.

```
# truss -t kaio,kaio create aio /dev/rdsk/c0t3d0s0                                                              = 9
kaio(5, 0xFFFFFF, 0xFFFFFF, 0xE6F68B50, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0xFFEFEB10, 0x00000000)                                                                = 2
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio_create(3, 0xFFEFF19, 1024, 0xFFEFB590)                                     = -268438128
kaio (AIOWAIT, 0x00000000)
aio succeeded
```

Note that you run this as root because it's reading directly from a raw device-specific file. On the command, the -t flag is specified with truss to instruct truss to trace only the kaio and lwp_create system calls.

The example used a raw device-specific file as the argument to the aio program. You have to specify a full path name for the file when you invoke aio). truss(1) output shows a kaio system call, followed by two lwp_create calls, and two more entries into the kaio routine to do the actual read, followed by the aiwait. The last line is the output from the kaio (aio succeeded). In this example, kaio is in fact a supported facility for this I/O operation—the kaio call with the AIREAD flag did not return an error.

In the example, kaio is not supported for the I/O.

```
# truss -t kaio,kaio create junkfile
kaio(5, 0xFFFFFF, 0xFFFFFF, 0xE6F68B50, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0xFFEFEB10, 0x00000000)                                                                = 0
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFF0188, 1024, 000B558)                                 0#48 ENOTSUP
lwp_create(000EDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
0io (AI0IT, 000188, 1024, 000B558)                                 0#48 ENOTSUP
lwp_create(000EDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
0io (AI0IT, 000188, 1024, 000B558)                                 0#48 ENOTSUP
lwp_create(000EDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
0io (AI0IT, 000188, 1024, 000B558)                                 0#48 ENOTSUP
lwp_create(000EDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
0io (AI0IT, 000188, 1024, 000B558)                                 0#48 ENOTSUP
lwp_create(000EDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
0io (AI0IT, 000188, 1024, 000B558)                                 0#48 ENOTSUP
lwp_create(000EDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0)
aio succeeded
```

Note that you run this as root because it's reading directly from a raw device-specific file. On the command, the -t flag is specified with truss to instruct truss to trace only the kaio and lwp_create system calls.

The example used a raw device-specific file as the argument to the aio program. You have to specify a full path name for the file when you invoke aio). truss(1) output shows a kaio system call, followed by two lwp_create calls, and two more entries into the kaio routine to do the actual read, followed by the aiwait. The last line is the output from the kaio (aio succeeded). In this example, kaio is in fact a supported facility for this I/O operation—the kaio call with the AIREAD flag did not return an error.

In the example, kaio is not supported for the I/O.

Once you have the test program compiled, use the truss(1) command to do a system-call trace of the execution path.

In this example, kaio is in fact a supported facility for this I/O operation—the kaio call with the AIREAD flag did not return an error.

In the example, kaio is not supported for the I/O.

It’s clear that the user-threads implementation results in more thread/LWP creation, which adds overhead and reduces efficiency. Why does the Solaris environment create 11 LWPs for a single async I/O? Why does the answer have to do with the initialization of async I/O library.

The first time an airead(3) or aiowrite(3) is called, an async I/O initialization routine is called and creates several worker threads to do async I/Os. The system is simply getting ready to process several I/Os and thus creates four reader LWPs and four writer LWPs, with one thread to do file sync. That accounts for the nine successful lwp_create calls you see above. If you were to add a second airead(3) or aiowrite(3) to the test program and rerun it with the truss(1) command, you wouldn't see all the lwp_creates for the second async I/O. The library handles subsequent async I/O requests with the worker threads created during initialization (though it will, of course, create more worker threads to keep up with the level of incoming async I/O requests).

Although the creation of a pool of worker threads up-front helps provide scalability for the user-threads async I/O facility, it still involves more overhead and a longer code path than does kernel async I/O.

## 11.5 Memory Mapped File I/O

File I/O discussed so far is done with the read, write, and lseek system calls to perform I/O on behalf of a process and to copy the data to or from the process’s address space. The I/O is performed into a kernel buffer and then copied to the process’s address space, as illustrated in 11.3.
