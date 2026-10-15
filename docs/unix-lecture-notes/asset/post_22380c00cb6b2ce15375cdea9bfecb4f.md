
# NAME

This section gives the name or names of the entry and briefly states its purpose.

# SYNOPSIS

This section summarizes the use of the entry being described.

# DESCRIPTION

This section describes the functionality of the header.

# APPLICATION USAGE

This section is informative. This section gives warnings and advice to application developers about the entry. In the event of conflict between warnings and advice and a normative part of this volume of POSIX.1-2008, the normative material is to be taken as correct.

# RATIONALE

This section is informative. This section contains historical information concerning the contents of this volume of POSIX.1-2008 and why features were included or discarded by the standard developers.

# FUTURE DIRECTIONS

This section is informative. This section provides comments which should be used as a guide to current thinking; there is not necessarily a commitment to adopt these future directions.

# SEE ALSO

This section is informative. This section gives references to related information.

The important sections are NAME, SYNOPSIS, DESCRIPTION, and SEE ALSO.

For example

```
$ man stdlib.h
```

will display the man page for the header file <stdlib.h>. This is a useful feature. But if you do not know the name of the command that you need, nor the names of any files that might be useful or relevant, then you do not know which man page to read. UNIX systems provide various methods of overcoming this problem.

## 2.4.2 Man Page Searching

The most basic solution, guaranteed to work on all systems, is to use the search feature of the man command. To search for all man pages that contain a particular keyword in their one-line summaries in the NAME Section, you can type

```
$ man -k keyword
```

This will only work if the whatis database has been built when the man pages were installed however, so you are at the mercy of the system administrator. For example, typing

## 2.5 Digging Deeper into the who Command

The output of the manual search on the utmp file will look something like:

```
endutent [getutent] (3) - access utmp file entries
getutent          (3) - access utmp file entries
getutid [getutent] (3) - access utmp file entries
getutline [getutent] (3) - access utmp file entries
login              (3) - write utmp and wtmp entries
logout [login]     (3) - write utmp and wtmp entries
pututline [getutent] (3) - access utmp file entries
sessreg            (1x) - manage utmp/wtmp entries for non-init clients
setutent [getutent] (3) - access utmp file entries
utmp               (5) - login records
utmpname [getutent] (3) - access utmp file entries
utmpx.h [utmpx]    (0p) - user accounting database definitions
wtmp [utmp]        (5) - login records
```

The first word is the topic of the man page, the next, the man page title, the third is the section number of the manual, and the last is a brief description of the topic.

Every UNIX system has a manual volume that deals with the files used by the commands. The number may vary. From the above output, it appears that the utmp file is described in Section 5 of the man pages:

```
utmp [utmp] (5) - login records
```

Also, the line

```
wtmp [utmp] (5) - login records
```

shows that the man page describing the wtmp file is the same page as the one describing utmp. Obviously, there is a man page for utmp in Section 5 of the manual. To specify the specific section to display, you need to specify it as an option. The syntax varies; in RedHat Linux either of these will work:

```
$ man 5 utmp
$ man -S5 utmp
```

There was also a line of output

```
utmpx.h [utmpx] (0p) - user accounting database definitions
```

The `<utmpx.h>` header file describes a POSIX-compliant interface to the utmp file. This interface is different from that of the `<utmp.h>` file. We will use the (outdated) `<utmp.h>` interface for our initial attempts, exploring the utmp file in greater depth, starting with the man page that our system delivers when we type either of the above man commands. After that we will consider using two other interfaces, the POSIX utmpx interface and a GNU extension, the thread-safe functions `getutent_r()` and its cousins.

The beginning of the man page for utmp from RedHat Enterprise Linux Release 4 is displayed below.

```
NAME
    utmp, wtmp - login records

SYNOPSIS
        #include <utmp.h>

DESCRIPTION
        The utmp file allows one to discover information about who is currently
        using the system. There may be more users currently using the system,
        because not all programs use utmp logging.

        Warning: utmp must not be writable, because many system programs
        (foolishly) depend on its integrity. You risk faked system logfiles and
        modifications of system files if you leave utmp writable to any user.
        The file is a sequence of entries with the following structure declared
        in the include file (note that this is only one of several definitions
        around; details depend on the version of libc):

        (lines omitted here)
```

First note that it tells us which header file is relevant: `<utmp.h>` This is the header file that the compiler will use when the include directive `#include <utmp.h>` is in your program⁶. Next, it issues a warning to system administrators to leave the file writable by anyone other than its owner, the superuser. Then it warns the rest of us, before showing us the contents of the include file, that the contents may differ from one installation to another.

Since UNIX is a free, community supported operating system, it has been evolving over time. You may find that what is described in a book, or in these notes, is different from what you observe on your system. It is not that anything is correct or incorrect, but that UNIX is a moving target, and that systems can differ in minor ways. For example, the man page for utmp in an older version of Linux will be very different from the one shown here. Even the location of the utmp file itself is different. Later versions of UNIX added system functions to provide a data abstraction layer so that the programmer would not need to know the actual structure of the file. The problem was that different versions of UNIX had different definitions of the utmp structure, and programs that accessed the structure directly were failing on different systems.

⁶There may be many files named `utmp.h` in the file system. Each compiler will have its own method of deciding which one to use. The GNU compiler collection (gcc) installs its own header files in specific places, and it uses these by default. The default search path used by gcc is typically

`/usr/local/include`
`target-install-dir/include`
`/usr/include`

where `target-install-dir` is the directory in which gcc was installed on the machine. This is explained in more detailed shortly.
