
## 3.10 waitpid(3)

The LSB has deprecated the use of waitid(3). Applications should call the waitpid(3) interface as specified in the Single UNIX Specification, but implementations need not support the X/Open System Interfaces Extension (XSI) functionality of WCONTINUED or WIFCONTINUED (Example 3.6).

### 3.11 PARSING OF COMMAND OPTIONS

The GNU getopt(3) function parses command-line arguments as specified by the Single UNIX Specification Version 3, when the plus sign “+” is the first character in the option string of the function’s third parameter.

The GNU option string flags “W;” (to enable long options), “-” (to return ‘\1’ for invalid options), and “::” (to enable optional flag arguments) should not be used when trying to maintain SUSv3 compliance (Example 3.7).

### 3.12 LSB DON'TS

This chapter is about portability etiquette. As an open systems developer, there are things you should not do. You should realize that the compromises to ensure portability outweigh the short-term benefits of tuning to a specific release.

#### 3.12.1 /proc

The LSB only specifies the /proc/cpuinfo file and its keys. Applications should not attempt to collect any other data from the /proc filesystem, because it is unspecified and unreliable.

### Example 3.6: Using waitpid(3)

```c
#include <assert.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>

int main (void)
{
  int rc, status;
  pid_t pid;

  pid = fork();

  if (pid < 0) {
    perror ("fork");
    exit (1);
  }

  if (0 == pid) {
    printf ("\tChild process (pid=%d) running\n", getpid());
    sleep (10);
    printf ("\tChild process (pid=%d) terminating\n", getpid());
    exit (0);
  }

  printf ("Parent process (pid=%d) waiting for child (pid=%d)\n",
         getpid(), pid);

  rc = waitpid (pid, &status, 0);

  printf ("Parent process (pid=%d) continuing ", getpid());
  printf ("after the termination of child (pid=%d).\n", pid);
  printf ("Status = 00%x  Return Code=%d\n", status, rc);

  if (rc < 0) {
    perror ("waitpid");
    exit (2);
  }

  exit (0);
}
```

### Example 3.7: Command Options

```c
#include <unistd.h>
#include <stdio.h>

int
main (int argc, char **argv)
{
    int aflag = 0;
    int bflag = 0;
    char *cvalue = NULL;
    int errflg = 0;
    int index, c;

    /* the plus sign is required to permanently set
     * POSIXLY_CORRECT
     */

    while ((c = getopt (argc, argv, "+abc:")) != -1)
    switch (c) {
        case 'a':
            aflag = 1;
            break;
        case 'b':
            bflag = 1;
            break;
        case 'c':
            cvalue = optarg;
            break;
        case ':':
            fprintf (stderr,
                "Option -%c requires an operand\n",
                optopt);
            errflg++;
            return 1;
        case '?':
            fprintf (stderr, "Unknown option -%c\n", optopt);
            errflg++;
            return 1;
        default:
            fprintf (stderr, "Hopelessly lost\n");
            errflg++;
            break;
    }

    if (errflg) {
        fprintf (stderr, "USAGE: %s -a -b -c file", argv[0]);
        exit(1);
    }
    printf ("aflag = %d, bflag = %d, cvalue = %s\n",
            aflag, bflag, cvalue);
    for (index = optind; index < argc; index++)
        printf ("Operand argument %s\n", argv[index]);
    exit(0);
}
```

#### 3.12.2 Berkeley Database

The Berkeley Database (DB)^4 is a popular data management engine used by many Linux applications; however, at the time of publication of this book, DB does not meet the LSB Futures selection criteria.^5

^4 Sleepycat Software, makers of Berkeley DB (http://www.sleepycat.com/).
^5 http://www.linuxbase.org/futures/criteria/

#### 3.12.3 Kernel

The Application Programming Interfaces (APIs) provided by the system libraries abstract the operating system resource management of the kernel. It is improper for a portable application to use the private interfaces of a system, so you should take care to only code with the interfaces defined by the LSB Written Specification.

#### 3.12.4 Drivers

On UNIX and GNU/Linux systems, “a file is a file”, and a device is just another file that can be opened, read from, written to, and closed. An application should not try to mimic the functionality of a driver; it must simply interact with the device in the protocol of the driver.

#### 3.12.5 Desktop

When developing an application that uses a Graphical User Interface (GUI), it is best to concentrate on perfecting its usability and portability rather than desktop integration. No one can guarantee a specific window manager or desktop that the end user will be using, so it is best to not limit the application by loading it down with desktop-specific features.

#### 3.12.6 Threads

At the time of the writing of this book, the current Linux distributions were in various states of supporting Linux threads, Next Generation POSIX Threads (NGPT), and Native POSIX Threads Library (NPTL). The next generation of Linux distributions will be supporting NPTL. LSB v2.0 specifies pthreads as implemented by NPTL and the 2.6 Linux kernel. Applications and middleware should migrate to NPTL.

#### 3.12.7 gets(3)

Although `gets(3)` is specified by POSIX, the LSB has deprecated it. Both the LSB and POSIX recommend the use of `fgets(3)` instead of `gets(3)`.

#### 3.12.8 system(3)

The LSB has its own definition of `system(3)` which does not reference ISO/IEC 9945. Although it is specified, for portability it is recommended instead to use `popen(3)`, `execl(3)`, `execle(3)`, or `execv(3)`.

#### 3.12.9 ncurses

Both the LSB and the SUS specify the use of `curses.h`. For source code portability, do not use `ncurses.h`.

#### 3.12.10 malloc(3)

When using `malloc(3)`, include `stdlib.h` instead of `malloc.h` because, along with compiler option -lmalloc, these are later used for debugging (Example 3.8).

### Example 3.8: `malloc(3)`

```c
#ifndef DEBUG
#include <malloc.h>
#endif
#include <stdlib.h>
```

## CHAPTER FOUR Packaging Your LSB Application

The LSB specifies application packaging in order to ensure compatibility between applications and Linux distributions. Packaging can be distribution-specific, so it is possible that your application will not run across distributions if you do not follow the LSB packaging specifications. In this chapter you will learn about the RPM file format and the correct locations for installing your applications.

### 4.1 Using RPM for PACKAGING

There are over one hundred Linux distributions for end users to run their applications on.^1 To ensure that applications will be able to install successfully, the LSB specifies the RPM file format as the best possible solution. It is the responsibility of an LSB Certified Runtime Environment (that is, an operating system or Linux distribution) to be able to install RPM packaged applications. The book *Maximum RPM* by Edward Bailey and the RPM Web site^2 are excellent resources for learning to create RPM packages. For the examples in this chapter, don’t worry about the details, but pay attention to the guidelines on where to install everything.

^1 DistroWatch (http://www.distrowatch.org/).
^2 http://www.rpm.org/

For reliability, an application cannot be dependent on itself for installation because ad hoc installers are not guaranteed to work. The RPM file format has been specified because it is accepted by many Linux distributions; however, you may use another packaging format if the install program your application is dependent on is LSB-certified and known to be previously installed.^3

^3 Portions of this chapter were derived with permission from “Where to Install My Products on Linux” by George Kraft IV, *Linux Journal*, November 2000.

#### 4.1.1 RPM Checking

The LSB package check command, **lsbpackchk**, is a program that verifies that a package and its contents conform to the LSB Written Specification. The version number it displays refers to the version of the specification that it was built for, not the version of the command itself.

### 4.2 INSTALLING YOUR APPLICATION IN THE RIGHT PLACE

Software developers and independent software vendors (ISVs) have differing ideas about the best place to install applications and software packages. Some install in `usr/bin/` or `usr/local/bin/`, others prefer the `/opt/` directory. Your preferences might vary depending on whether you come from a UNIX System V, Berkeley Software Distribution (BSD), or GNU/Linux background. These unpredictable variations cause file and directory naming conflicts that sometimes disrupt software installation, removal, and upgrades.

The Filesystem Hierarchy Standard (FHS),^4 referenced by the LSB, provides guidelines and defines requirements for file and directory placement. The FHS promotes the interoperability of applications, system administration tools, development tools, and scripts. The FHS explains in detail the content and purpose of each of the primary directories. Figure 4.1 shows the directory structure as specified by the FHS.

^4 http://www.pathname.com/fhs/

In addition to the FHS, the System V Application Binary Interface,^5 the Intel Binary Compatibility Standard V.2 (iBCS2), the Common Operating System Environment (COSE), the Linux Standard Base (LSB), and the UNIX

^5 System V Application Binary Interface, Dec. 17, 2003, The SCO Group (http://www.caldera.com/developers/gabi/2003-12-17/contents.html).
