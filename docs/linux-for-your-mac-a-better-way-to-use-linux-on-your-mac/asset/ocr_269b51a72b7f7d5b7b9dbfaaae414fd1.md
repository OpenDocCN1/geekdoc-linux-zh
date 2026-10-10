# Choosing a Shell

# pksh or ksh?

The original KornShell was first developed by David G. Korn in 1983 while at AT&T Bell Laboratories. Other versions followed in 1986, 1988, and 1993. The current ksh shell is known as *ksh93*. The public-domain version of ksh included with many Linux systems, (also known as *pdksht*), closely follows the 1988 version of the KornShell.

The good news is that as of March 1, 2000, AT&T decided to open and release the source to *ksh93*, and to make various binary distributions available for download (see the section “Resources” at the end of this chapter for the Web site).

Two other famous shells mimicked by *bash* and *tcsh* on Linux systems are the Bourne shell by Steven Bourne at AT&T Bell Laboratories, and the C shell, programmed by Bill Joy while at the University of California.

Like *bash*, the *ksh* shell will use a custom resource file named `.profile` in a user’s home directory, with system-wide defaults located in `/etc/profile`.

# tcsh

The *tcsh* shell, created by more than fifty developers, closely mimics the original C shell crafted by Bill Joy for BSD (*Berkeley Software Distribution*) UNIX. Paralleling the other shells detailed in this section, *tcsh* hosts all the features one would expect of a modern shell. This includes job control, aliases, history, command-line editing, command completion, and more.

System-wide defaults are stored in `/etc/csh.cshrc`/`/etc/csh.login` (which contains values read in by *csh* after a user logs in), and `/etc/csh.logout` (read in after a user logs out). Custom files in a user’s home directory are `.cshrc`, `.tcshrc`, `.login`, and `.logout`.

# zsh

The Z shell, known as *zsh*, was written by Paul Falstad while at Princeton, and is based on *sh*, also known as the Bourne shell (named after its developer, S.R. Bourne). Like other shells discussed here, *zsh* has many, if not more, features than one may need for conducting productive sessions at the Linux console.

The *zsh* shell has one of the most complete feature sets of all shells, including advantages over *bash* such as logout actions. Like *pksh*, it has nearly complete compatibility with the 1988 version of the KornShell.