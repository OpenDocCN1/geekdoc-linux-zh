I remember when these export controls first went into effect around 1981 and my company, Onyx, had to split our UNlX distribution into two versions, a full domestic one and an international one that was devoid of the decryption library and program.

Note that one-way encryption is allowed (because it cannot be used to "hide" information) so the UNlX/Linux password encryption remained legal.

PGP may be downloaded from the following site:

http://web.mit.edu/network/pgp.html

# C.5.7 GNU Privacy Guard (GPG)

The GNU Privacy Guard, GPG, is the Free Software Foundation's Open Source implementation of Philip Zimmermann's Pretty Good Privacy. It was first available in late 1999. It does not suffer from the licensing and export restrictions of PGP. It may be legally downloaded (by anyone) from

www.gnupg.org/

# C.5.8 The tcpdump Utility

One of the U.S. government's energy and nuclear research laboratories, Lawrence Berkeley Lab (LBL), offers the tcpdump Linux/UNIX utility. This utility is a sniffer intended for System Administrators to analyze their computers and networks for both general network problems and security problems. As such, it does not show enough of the packet to, say, see the contents of a mail message (though it would be trivial to alter this). I also have found it quite useful in debugging during development of client/server software. The tcpdump program and related software may be downloaded from the laboratory at the URLs listed below. It is easy to set up and use.

ftp://ftp.ee.lbl.gov/libpcap.tar.Z
ftp://ftp.ee.lbl.gov/pcapture-0.2.1.tar.Z
ftp://ftp.ee.lbl.gov/tcpdump-3.4.tar.Z

# C.5.9 The Ethereal GUI-Based Sniffer

This is an open-source GUI-based sniffer that besides the "show every packet" philosophy of tcpdump allows easy watching of a particular session. It allows observing the actual data so honesty in its use is important here. It even allows decompressing gzipped streams. It is the author's favorite sniffer.