# Chapter 14. Programming Tools

TelCheck (and frink) can save you hours of time you'd otherwise spend staring at your code and counting braces.

TelCheck is distributed as C source code with a Makefile. Like frink, it will compile under Windows if you get a copy of Gnu getopt.c to link with it.

# 14.2.2 ICE Tcl_lint

| Language | executable |
| Primary Site | http://icemcfd.com/tcl/ice.html |
| Contact | tcl@icemcfd.com |
| Tcl Revision Supported | Tcl: 7.3-8.1 Tk: 3.6-8.1 |
| Supported Platforms | DEC OSF V4.0, HP-UX 9.01, 10.0, IBM AIX 3.2, 4.0, 4.1, Slackware Linux 2.3.30 (ELF), SGI IRI 5.x and above, Sparc Solaris 5.3 and up, Windows NT 4.0 and Win95

The tcl_lint program is part of the ICEM Tcl compiler package. It can be licensed without charge for the preceding platforms.

This program uses the same sophisticated parser as the ICEM Tcl compiler and does an excellent job of detecting many different types of errors, including:

+   - Parsing errors.
- Unset or nonexistent variables.
- Incorrect usage of built-in and user-defined procedures.
- Possibly illegal arithmetic statements.
- A control command with an empty body.
- A nonparsable statement.
- Using a routine that has an implicit return in a command substitution.

The next example has the the following errors, which are detected by tcl_lint:
- this_does_not_yet_exist has no value to be returned by set.
- Both expr statements are illegal.