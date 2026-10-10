# IPX (AF_IPX)

The IPX protocol is most commonly utilized in Novell NetWare(tm) local area network environments. Linux includes support for this protocol and may be configured to act as a network endpoint, or as a router for IPX.

**Kernel Compile Options:**

```
Networking options --->
[*] The IPX protocol
[ ] Full internal IPX network
```

The IPX protocol and the NCPFS are covered in greater depth in the IPX-HOWTO (see IPX-HOWTO.html).

# NetRom (AF_NETROM)

NetRom device names are "nr0", "nr1", etc.

**Kernel Compile Options:**

```
Networking options --->
[*] Amateur Radio AX.25 Level 2
[ ] Amateur Radio NET/ROM
```

The AX25, Netrom, and Rose protocols are covered by the AX25-HOWTO (see http://metalab.unc.edu/LDP/). These protocols are used by Amateur Radio Operators worldwide in packet radio experimentation.

Most of the work for implementation of these protocols has been done by Jonathon Naylor <jsn@cs.nott.ac.uk>.

# Rose Protocol (AF_ROSE)

Rose device names are "rs0", "rs1", etc. in 2.1.* kernels. Rose is available in the 2.1.* kernels.

**Kernel Compile Options:**

```
Networking options --->
[*] Amateur Radio AX.25 Level 2
<*> Amateur Radio X.25 PLP (Rose)
```

The AX25, Netrom, and Rose protocols are covered by the AX25-HOWTO (see http://metalab.unc.edu/LDP/). These protocols are used by Amateur Radio Operators worldwide in packet radio experimentation.