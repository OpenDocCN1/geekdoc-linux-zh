not constitute a standard of a national or international organization such as ANSI,
DIN or ISO, but an agreement between Internet users.

Because of the free availability of RFCs, implementation is possible for\very. This is one of the reasons for the diffusion of the protocol and its good
cross-compatibility between different implementations. RFCs are developed by
experienced Internet users and system administrators; the IAB (Internet Activities
Board) manages these standards and their development.

RFCs can be easily written by any interested Internet user. The definition
of a stable and secure protocol is, however, relatively complex, so only a few
users would state the process of public discussion. Many of the RFCs are
elaborated by the IETF (Internet Engineering Task Force). The process of how an
RFC becomes an Internet standard is also defined in RFCs (rfc1311) and
[rfc1602].

If you want to delve deeper into UNIX networks, the Internet or intranets,
you must read the corresponding RFCs. A list of the most important RFCs can be
found in the RFC directory in Appendix D; in addition, we always refer to the
corresponding RFCs where necessary. The RFCs can be found, for example,
under `http://ftp.nic.de/pub/doc/rfc`, `http://ftp.gwd.de/pub/rfc`, or `http://ftp.ietf.org/rfc`.

Because of the complexity of networks and the employed software, this
book is not able to cover all aspects. A great deal of additional information can be
found in the HowTo of the Linux Documentation Project, for example
on PPP, news or mail, and in the FAQs of the newsgroups that deal with these
subjects. Many of the programs used under LINUX are not LINUX-specific and are
therefore not discussed in the LINUX newsgroups, but in those on the programs or
protocols. Furthermore, the bibliography in Appendix C contains a list of useful
books on this subject area.

The current Windows versions include clients for `telnet` and
`ftp`; for practically all other protocols, free clients are Available. But
very little known, there is an NFS server (SOSS) and a client (XFS) for DOS.

The use of Windows as an Internet server is not to be recommended, but as a
client, Windows is often an alternative to LINUX or UNIX. The latest versions of
is popular PC operating system usually include all Internet clients needed.

# 13.1 Network software layers

The TCP/IP software consists of a number of layers that build on each other.
Each layer is based on a well-defined interface with the underlying layers and can
make use of other layers' services without knowing which means are employed
to provide these. Thus, it does not matter at all to an program which