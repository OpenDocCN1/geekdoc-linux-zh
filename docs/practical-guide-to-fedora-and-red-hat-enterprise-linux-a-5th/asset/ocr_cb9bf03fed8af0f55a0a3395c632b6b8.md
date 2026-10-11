# apropos: SEARCHES FOR A KEYWORD

When you do not know the name of the command you need to carry out a particular task, you can use *apropos* with a keyword to search for it. This utility searches for the keyword in the short description line (the top line) of all *man* pages and displays those that contain a match. The *man* utility, when called with the `-k` (keyword) option, provides the same output as *apropos* (it is the same command).

The database *apropos* uses, named *whatis*, is not available on Fedora/RHEL systems when they are first installed, but is built automatically by *cron* (page 365) using *makewhatis*. (The *cron* utility runs the `/etc/cron.daily/makewhatis` *cron* script to build the *whatis* database.) If you turn the system off periodically (as with a laptop), the script may not be run. If *apropos* does not produce any output, run the command `makewhatis -w` while working with root privileges.

The following example shows the output of *apropos* when you call it with the **who** keyword. The output includes the name of each command, the section of the manual that contains it, and the brief description from the top of the man page. This list includes the utility that you need (**who**) and identifies other, related tools that you might find useful:

```
$ apropos who
at.allow (5)
	- determine who can submit jobs via at or batch
at.deny (5)
	- determine who can submit jobs via at or batch
from (1)
	- print names of those who have sent mail
w (1)
	- Show who is logged on and what they are doing.
w,procs (1)
	- Show who is logged on and what they are doing.
who (1)
	- show who is logged on
whoami (1)
	- print effective userid
whois (1)
	- client for the whois directory service
```

**whatis** The *whatis* utility is similar to *apropos* but finds only complete word matches for the name of the utility:

```
$ whatis who
who
(1) - show who is logged on
```

# info: DISPLAYS INFORMATION ABOUT UTILITIES

The textual *info* utility is a menu-based hypertext system developed by the GNU project (page 2) and distributed with Fedora/RHEL. The *info* utility includes a tutorial

# man and info display different information

> The *info* utility displays more complete and up-to-date information on GNU utilities than does *man*. When a man page displays abbreviated information on a utility that is covered by *info*, the man page refers to *info*. The *man* utility frequently displays the only information available on non-GNU utilities. When *info* displays information on non-GNU utilities, it is frequently a copy of the *man* page.