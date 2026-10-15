# Network Security

You should be aware of two broad problems in network security: snooping on the Net and trusting the wrong server. Snooping is a problem in any site that allows arbitrary users to collect packets. This system, as discussed so far, can allow someone to capture all the keystrokes of a user changing his or her password. This is as bad as someone snooping a telnet session and watching you change your password. Trusting the wrong server is a problem because the use of any of the r-commands requires root .rhosts files on various machines, and the use of NFS requires the export of sensitive files.

Both problems, however, are eminently solvable. If you already have worked out what the .rhosts or exports implications are for your organization, you merely need to check to ensure that allowing rsh and NFS to support password update doesn’t break your trust rules. If you are small, at home, or behind a firewall, you probably don’t have a lot to worry about. And if you do need secure, untappable, and trusted channels to selected machines, you can use several programs to make encrypted connections to other machines: either ssh, the Secure SHell, or the new skip program of the IETF.

# Listing 15.4 (continued)

```
sayWriteError(name,errno) char *name; int errno; {

(void) fprintf(stderr, "%s: Error writing and closing output
file "%s". %s (errno %d), halting.\n",
ProgName, name, (errno < sys_nerr)?
sys_errlist[errno]: "Unknown error", errno);
(void) fprintf(stderr, "%s: please inspect and remove remnant
of "%s".\n", ProgName,name);
return;
}
```