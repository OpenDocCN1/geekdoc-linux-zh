tions will be held back by old standards. For instance, there are millions of users still enduring short file names required by MS-DOS. Other users enjoy using the longer file names permitted by Unix, Macintosh, Windows NT, and other systems.

# POSIX

POSIX (the IEEE${ }^{2}$ Standard Portable Operating System Interface for Computer Environments) describes system calls in terms of C language data definitions and subroutine calls.

The POSIX standard is permissive in that it allows the system to offer additional features not required by the standard. The POSIX standard urges, but does not require, non-standard features to be documented.

There is a subtle point that must be noted: the standard does not describe the system, but rather it says a conforming implementation “shall support all required interfaces defined within this standard. These interfaces shall support the functional behavior described herein[3].” As a result, a *strictly conforming* POSIX application (one which does not use features outside the standard) will need no modification to run on the system.

# A cautionary example

Even though standards may not exhaustively describe the system’s behavior, a careful programmer pays attention to the standard. Relying on the apparent behavior of the system can lead to trouble when moving an application to a different implementation of the same system.

A case in point relates to the `timeout` value in the `select` call available on a number of Unix systems. This call allows the program to wait for I/O activity on any of a number of ports or the expiration of a timeout.

The documentation for this call often contains the comment in the BUGS section:

> select() should probably return the time remaining from the original timeout, if any, by modifying the time value

${ }^{2}$Institute of Electrical and Electronic Engineers