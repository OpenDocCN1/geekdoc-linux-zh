There’s a good DNS glossary at:

+   http://www.menandmice.com/ONLINE%20DOCS%20AND%20FAQ/Glossary/index.htm

Stevens, Chapter 14 covers the DNS although it’s more a theoretical than a practical treatment. Many people recommend

+   Paul Abilitz & Cricket Liu, DNS and BIND (O’Reilly, 2001)

# A little history

Before the DNS was invented, using the **hosts** file involved a lot of centralized administration, and it inhibited change on the net because in practice almost every local copy of HOSTS.TXT was out of date to a greater or lesser extent. (RFC-799 in 1981 said that with 400 machines on the network, managing the **hosts** file was becoming “awkward”). When the DNS was introduced it overcome these problems. The last list of hosts published as an RFC was:

+   RFC-1166 July 1990 *Internet Numbers*

The **hosts** file still exists on both Linux and Windows. It is useful when you don’t use DNS, i.e. on small or test networks, or networks not connected to the Internet. As we’ll see in the next chapter, keeping values in the **hosts** file can cause confusion – they don’t change when you alter the corresponding DNS records. Assuming you have a regular network connected to the Internet, don’t use **hosts** unless you have to.

As we mentioned in Chapter 5’s Notes, there is a related file called **networks** although it is of debatable use. On Linux this is /etc/networks. On Windows-NT the files are stored in C:\winnt\system32\drivers\etc.

Microsoft Windows Networking also uses a special hosts file of its own called Lmhosts (“LAN Manager hosts file”, Chapter 19). You can store network names/numbers in the DNS although it’s rarely done:

+   RFC-1101 April 1989 *DNS Encoding of Network Names and Other Types*

# Domain naming

Hierarchical domains as we know them were proposed in

+   RFC-805 February 1982 *Computer Mail Meeting Notes*

A good discussion of the ideas behind the DNS is in:

+   RFC-819 August 1982 *The Domain Naming Convention for Internet User Applications*

For historical information and notes on the evolution of the DNS see:

+   RFC-830 October 1982 *A Distributed System for Internet Name Service*
+   RFC-883 November 1983 *Domain Names – Implementation And Specification*

The DNS specifications are:

+   RFC-1034 November 1987 *Domain Names – Concepts And Facilities*
+   RFC-1035 November 1987 *Domain Names – Implementation And Specification*