
- Comment at the level you yourself will find helpful when you return to the script after a month or two. Some useful points to comment on are the following: choices of algorithm, reasons for not doing things in a more obvious way, unusual paths through the code, anything that was a stumbling block during development. Don't clutter code with useless comments; assume intelligence and language proficiency on the part of the reader.

- Code comments work best at the granularity of blocks or functions. Comments that describe the function of a variable should appear with the variable's declaration or first use.

- It's OK to run scripts as root, but avoid making them setuid; it's tricky to make setuid scripts completely secure. Use sudo to implement appropriate access control policies instead.

- With bash, use -x to echo commands before they are executed and -n to check commands for syntax without executing them.

- Perl's -w option warns you about suspicious behaviors such as variables used before their values are set. You can include this option on a script's shebang line or turn it on in the program's text with use warnings.

- In Python, you are in debug mode unless you explicitly turn it off with a -O argument on the command line. That means you can test the special __debug__ variable before printing diagnostic output.

Tom Christiansen suggests the following five Golden Rules for producing useful error messages:

- Error messages should go to STDERR, not STDOUT.
- Include the name of the program that's issuing the error.
- State what function or operation failed.
- If a system call fails, include the perror string ($! in Perl).
- Exit with some code other than 0.

Perl makes it easy to follow all five rules:

```
die "can't open $filename: $!";
```

## 2.7 RECOMMENDED READING

BROOKS, FREDERICK P., JR. The Mythical Man-Month: Essays on Software Engineering. Reading, MA: Addison-Wesley, 1995.

### Shell basics and bash scripting

ALBING, CARL, JP VOSSEN, AND CAMERON NEWHAM. Bash Cookbook. Sebastopol, CA: O'Reilly Media, 2007.

KERNIGHAN, BRIAN W., AND ROB PIKE. *The UNIX Programming Environment.* Englewood Cliffs, NJ: Prentice-Hall, 1984.

NEWHAM, CAMERON, AND BILL ROSENBLATT. *Learning the bash Shell (3rd Edition),* Sebastopol, CA: O'Reilly Media, 2005.

POWERS, SHELLEY, JERRY PEEK, TIM O'REILLY, AND MIKE LOUKIDES. *Unix Power Tools, (3rd Edition),* Sebastopol, CA: O'Reilly Media, 2002.

### Regular expressions

FRIEDL, JEFFREY. *Mastering Regular Expressions (3rd Edition),* Sebastopol, CA: O'Reilly Media, 2006.

GOYVAERTS, JAN, AND STEVEN LEVITHAN. *Regular Expressions Cookbook.* Sebastopol, CA: O'Reilly Media, 2009.

### Perl scripting

WALL, LARRY, TOM CHRISTIANSEN, AND JON ORWANT. *Programming Perl (3rd Edition),* Sebastopol, CA: O'Reilly Media, 2000.

SCHWARTZ, RANDAL L., TOM PHOENIX, AND BRIAN D FOY. *Learning Perl (5th Edition),* Sebastopol, CA: O'Reilly Media, 2008.

BLANK-EDELMAN, DAVID. *Automating System Administration with Perl,* Sebastopol, CA: O'Reilly Media, 2009.

CHRISTIANSEN, TOM, AND NATHAN TORKINGTON. *Perl Cookbook (2nd Edition).* Sebastopol, CA: O'Reilly Media, 2003.

### Python scripting

BEAZLEY, DAVID M. *Python Essential Reference (4th Edition),* Reading, MA: Addison-Wesley, 2009.

GIFT, NOAH, AND JEREMY M. JONES. *Python for Unix and Linux System Administrators,* Sebastopol, CA: O'Reilly Media, 2008.

MARTELLI, ALEX, ANNA MARTELLI RAVENSCROFT, AND DAVID ASCHER. *Python Cookbook (2nd Edition),* Sebastopol, CA: O'Reilly Media, 2005.

PILGRIM, MARK. *Dive Into Python.* Berkeley, CA: Apress, 2004. This book is also available for free on the web at diveintopython.org.

## 3 Booting and Shutting Down

![](img/14d78e3cecac4581d37024baf1e94cca_125_0.png)

Like most things UNIX, system startup and shutdown have matured into carefully engineered processes that accommodate many possible contingencies. As administrators, we negotiate the intricacies of the boot process to prevent and troubleshoot problems. An effective sysadmin understands the fundamentals first.

Bootstrapping has always been somewhat mysterious, but it was simpler in the days when manufacturers controlled every aspect of the system’s hardware and software. Now that we have Linux and Solaris running on PC hardware, the boot procedure has to play by PC rules and deal with many potential configurations. Although we discuss the boot procedure for all our example systems in this chapter, you’ll see that we have quite a bit more to say about the PC-based versions of UNIX than about the “captive” systems.

This chapter appears early in the book, but it refers to material that is not discussed in detail until many hundreds of pages later. In particular, familiarity with the material in Chapter 6, *The Filesystem*, and Chapter 13, *Drivers and the Kernel*, will prove helpful.
