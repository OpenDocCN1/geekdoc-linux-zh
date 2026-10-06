# Name (Continued)

POSIX 2003.2 (POSIX.3.2) | Test methods for POSIX 1003.2.

POSIX 1003.9 (POSIX.9) | FORTRAN binding to 1990 version of 1003.1.

POSIX 1003.17 (POSIX.17) | Standard for X.500 Directory Services, a protocol that allows multi-
ple distributed "directories" to be searched as a single entity. The
word "directory" does not refer to a GNU/Linux filesystem
but to a generic database.

POSIX 1387.2 | System administration: software management (principally a soft-
ware installation standard).

Issues related to system administration are specifically excluded from POSIX.1,
as are implementation details. After all, an application program does not know
how to create a new device special file and does not care how the open()
function (which opens a file) works internally. By avoiding implementation issues,
t standard allows systems that are not based on UNIX to conform to POSIX.1.

The POSIX.1 committee was responsible for codifying existing practice, not-
engineering a new version of the UNIX system. During the development of the
POSIX.1 standard, partitions of BSD and System V were forced to reconcile
differferences. In some cases this meant standardizing on behavior one or
the other version. In some cases the working group decided that both the BSD and
System V implementations of some features were deficient and created new inter-
faces (such as terminal control) based on existing practice but with new syntax and
semantics. No compromise seemed to be reachable, the working group
adopt optional behavior. For example, BSD had job control at least since re-
lease4.1, whereas SVR3 does not support job control. POSIX.1 makes job control
an option.

One compromise took a unique form. POSIX.1 specifies for file ar-
ch. On UNIX System V, the preferred archive format is cpio (page 1124). On
BSD the preferred format is tar (page 1343). POSIX.1 requires that both formats are
supported, in slightly modified forms. Because the specification of utilities is outside
the scope of POSIX.1, neither the cpio nor the tar is mentioned; only the file
formats for the archives are part of the standard. POSIX.1 requires that the imple-
provide unnamed archive creation and reading utilities. See
page 1439 for a discussion of the pax utility specified by POSIX.2.

The POSIX.1 standard is available from the American National Standards In-
titute (ANSI) or from the IEEE. In addition, the standard has been adopted as an