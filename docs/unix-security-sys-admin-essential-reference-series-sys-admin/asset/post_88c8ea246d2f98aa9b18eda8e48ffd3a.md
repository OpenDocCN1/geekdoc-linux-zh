
## What Is Rootkit?

Properly, Rootkit's packing list includes the following items:

- an Ethernet sniffer, specialized for logging passwords;
- a Trojan login replacement with a back door;
- support programs that are direct replacements for UNIX utilities (e.g., `ps`, `netstat`, `ifconfig`) that could allow someone to detect the installed Ethernet sniffer; and
- a utility for installing the Trojan system programs with the same dates, permissions, UID, GID, and checksum as the file being replaced.

Some strains of Rootkit also include the following items:

- replacement programs for `ls` and `du`;
- replacements for `in.telnetd`; and
- Trojan replacements for `chfn`, `csh`, `inetd`, `top`, `rshd`, and `syslogd`.

## Rootkit Samples

I've analyzed seven different SunOS Rootkit samples and three Linux Rootkit samples. The SunOS variants fall into two distinct strains, and the Linux variants all belong to a single strain.

## SunOS Strains

The two SunOS strains can be characterized by the secondary utilities included for stealth, "smartness" of the Trojan system programs, number of cracking tools supplied, and bug fixes. Version 1 strains are the oldest and come with more secondary programs to hide the intruder, such as `zap`, `ls`, and `du` Trojan replacements. Version 2 strains are derived from the older version 1 strains. Version 2 strains fixed a number of bugs in the modified SunOS source code and changed the makeup of the support programs. For some reason, the stealth versions of `ls` and `du` were removed. However, several cracking tools were added, as described in Table 19.1.

The sniffer is the `Esniff.c` program from `Phrack Magazine` [Vol. 5, Issue 45, File 5 of 28: March 30, 1994 (ISSN 1068-1035)]. The sniffing buffer varies from 128 bytes to 1024 bytes. Various Rootkits call this `es`, `watch`, or `rpc.rarpd`. The `login`, `ps`, `netstat`, and `ifconfig` are hacked versions of Sun Microsystems's proprietary SunOS v4.1.x source code. They all read mask files to specify which output to hide. Version 1 strains hardcode the filenames `/dev/ptyX`, where X is a single lowercase letter (with `p`, `q`, and `r` being the most popular). Typically, SunOS v4.x `pty` device files are of the form `ptyld`, `q`, `r` followed by a hexadecimal digit, so it is very easy

not to notice these added files. In version 2 strains, the filenames are ns.f and ps.f in the data/ directory in which Rootkit is built. These mask files can be quite expressive. (See the sidebar "Mask File Formats" for examples.)

The login Trojan allows anyone to log in as root across the network when supplying the magic password. The earliest versions hardcoded this password. I've seen D13hhf and fasune. Later versions query for the password when installing Rootkit. Regardless of the method used, the login Trojan binary does not contain the password in plain text form (it could be found with strings). When the password is hardcoded, it is hidden from strings' view by assigning each letter to an element of a character array. When the password is picked during installation, the bitwise note of the password's letters is stored in the binary. The Trojan login then decrypts the magic password at runtime. Some of the login Trojans also store username password pairs in a file for later collection.

| Tool | Description |
|------|-------------|
| strobe | Julian Assange's (AKA Proff) super-optimized TCP port surveyor. The official distribution is ftp://suburbia.apana.org.au/pub/users/proff/original/strobe.tgz. |
| iss.sh | Christopher Klaus's Internet Security Scanner v1.21. The official distribution is ftp://ftp.iss.net/pub/iss/iss21.shar. |
| traceroute.c | Van Jacobson's well-known traceroute program. The official distribution is in ftp://ftp.ee.lbl.gov/. |
| nuke | A program to send an ICMP "host unreachable" packet to specified hosts. Posted periodically to the Usenet alt.2600 newsgroup. |
| nfs shell | Leendert van Doom's (leendert@cs.vu.nl) shell that provides access to NFS filesystems. |
| ypx | Rob J. Nauta's (rob@wzv.win.tue.nl) program to transfer NIS maps beyond a local network; posted to the Usenet alt.sources newsgroup. |
| bootparam | A program that can be used to determine default routers and other information about boot servers (SunOS proprietary code). |
