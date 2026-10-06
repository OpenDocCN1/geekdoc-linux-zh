# Printing

You can use mt to manipulate files on a multvolume dump tape. The following mt command positions the tape (fsf 2 instructs mt to skip past two files leaving the tape at the start of the third file). The restore command restores the /var filesystem from the previous example:

```
# mt -f /dev/st0 fsf 2
# restore rf /dev/st0
```

Unlike Microsoft operating systems, UNIX/Linux takes a simplistic approach to printers. You do not need to load special drivers to use a printer. Printers are simply attached to a serial or parallel port (directly to the network). Applications are responsible for generating output that will properly drive the printer. This choice makes operating system for printers very easy (at the expense of the application developer). The www.linuxprinting.org Web site, a good source of information on printers and printing under GNU/Linux, offers printer recommendations and hosts a support database with details about many printers, including notes and driver information. The site also has forums, articles and a HOWTO on

A printing system handles the tasks implicit in getting a print job from an application (or the command line) through a queue for a suitable printer and getting it printed. For example, some filters can convert PostScript files into files specific to a given model of printer by calling the ghostscript utility with the appropriate arguments. Some filters can automatically determine the type of input file and call the proper utility to convert it into the form needed by a certain printer. While handling a job, the printing system can also keep track of billing information so that printer accounts can be charged for use. When a printer fails, the printing system can redirect jobs bound for that printer to similar printers.

UNIX has traditionally two printing systems: the BSD Line Printer Daemon (lpd) and AT&T Line Printer (ip). GNU/Linux adapted those systems at first, and both UNIX and GNU/Linux have seen modifications to and replacements for these systems, notably LPRng. As of Red Hat 8.0, the default printing system is LPRng² running the Berkeley UNIX printer package (lpd/lp). In addition, Red Hat supports several printing systems, including CUPS (page 1010).

29. Even though LPRng is the default printing system under Red Hat 8.0, Red Hat has deprecated LPRng and will remove it in a future release. CUPS (page 1010) is expected to be the new default.