goal:

```
#  lpc topp lexiemark 186 182
```

# lprm

The lprm command allows you to remove a job or jobs from the spool queue of the default printer. You may pass a −P option with a printer name to specify a different printer. Entering the lprm command with the number of a job in the queue removes that job. You can also use lpq to see the job numbers in a queue, as described earlier.

Issuing lprm with an argument of − removes all jobs the initiator owns, clearing the queue entirely if issued by the superuser. If the superuser issues the lprm command followed by a username, all jobs for that user will be removed. Thus, if you wish to remove job 11 and you are the owner or the superuser, you may issue the following command:

```
$  lprm  11
```

If you're the superuser and you want to remove all the jobs owned by someone, you could enter the following command:

```
#  lprm  someone
```

# Alternative Printing Utilities

Red Hat 7.3 ships with LPRng and the rhs-printfilters package as the basic printing system and print filter set, respectively. CUPS is installed but doesn't get configured by default. These are not the only options available, however. In fact, some distributions default to alternative systems, such as the older lpd, the newer CUPS, or alternative magic filters. It's almost always easiest to use whichever package comes with your distribution, but you may want to consider replacing a package under some circumstances.

# Alternatives to LPRng

There are several spooling packages on the market. Traditionally, lpd has been the most popular, but Linux distributions are beginning to abandon it, for various reasons. One disadvantage is that the original lpd package's lpr, lpc, lpq, and lprm are each SGID commands, and all except lpc are also SUID. This means that anyone running these binaries temporarily assumes the privileges of the owner of the binary (SUID) or the group of the binary (GUID). This allows restricted access to resources that are not meant to be manipulated by the basic user. This is a potential security problem since any user who finds a way to break out of the program or to exploit some weakness in the program may use these privileges—especially if the user or group is root—to weak havoc system-wide.

There are also a great many things that a spooling program could do that lpd doesn't do. Among these are load balancing between different print queues and tighter authorization constraints. Nonetheless, you may still find yourself using lpd with some distributions. If you do, the preceding discussion of LPRng is applicable, aside from a few minor details like the exact format of lpq's output. LPRng is a more secure and streamlined package, and so is generally preferable to lpd.

LPRng is an enhanced version of the lpd package. It provides the lpr, lpc, and lprm programs in an implementation that requires much less overhead and doesn't require SUID root. It supports dynamic redirection of print queues, load balancing, automatic job holding, very clear diagnostics,