
You can run `no -a` to see a list of all the available variables—there are currently more than 125. Table 14.14 lists some of the ones with security implications.

## Table 14.14 Security-related TCP/IP tuning variables for AIX

| Variable | Meaning | Default |
|---|---|---|
| bcastping | Respond to broadcast pings | 0 |
| directed_broadcast | Allow forwarding of broadcast packets | 0 |
| ipforwarding | Allow IP forwarding | 0 |
| ipignoreredirects | Ignore ICMP redirects | 0<sup>a</sup> |
| ipsrcrouteforward | Forward source-routed IP packets | 1<sup>a</sup> |
| ipsrcrouterecv | Accept source-routed IP packets | 0 |
| ipsrcroutesend | Block sending of source-routed packets | 1 |

a. Probably advisable to change

To set a variable, use

```
no -p -o variable=value
```

For example, to prevent the TCP/IP stack from forwarding source-routed packets, you would use the command

```
aix$ sudo no -p -o ipsrcrouteforward=0
```

The `-p` option makes the change effective both immediately and after a reboot.

## 14.16 RECOMMENDED READING

- STEVENS, W. RICHARD. *TCP/IP Illustrated, Volume One: The Protocols*. Reading, MA: Addison-Wesley, 1994.

- WRIGHT, GARY R., AND W. RICHARD STEVENS. *TCP/IP Illustrated, Volume Two: The Implementation*. Reading, MA: Addison-Wesley, 1995.

These two books are an excellent and thorough guide to the TCP/IP protocol stack. A bit dated, but still solid.

- STEVENS, W. RICHARD. *UNIX Network Programming*. Upper Saddle River, NJ: Prentice Hall, 1990.

- STEVENS, W. RICHARD, BILL FENNER, AND ANDREW M. RUDOFF. *UNIX Network Programming, Volume 1, The Sockets Networking API* (3rd Edition). Upper Saddle River, NJ: Addison-Wesley, 2003.

- STEVENS, W. RICHARD. *UNIX Network Programming, Volume 2: Interprocess Communications* (2nd Edition). Upper Saddle River, NJ: Addison-Wesley, 1999.

These books are the student's bibles in networking classes that involve programming. If you need only the Berkeley sockets interface, the original edition is still a fine reference. If you need the STREAMS interface too, then the third edition, which includes IPv6, is a good bet. All three are clearly written in typical Rich Stevens style.

- TANENBAUM, ANDREW. *Computer Networks* (4th Edition). Upper Saddle River, NJ: Prentice Hall PTR, 2003.

This was the first networking text, and it is still a classic. It contains a thorough description of all the nitty-gritty details going on at the physical and link layers of the protocol stack. The latest edition includes coverage on wireless networks, gigabit Ethernet, peer-to-peer networks, voice over IP, and more.

- SALUS, PETER H. *Casting the Net: From ARPANET to Internet and Beyond*. Reading, MA: Addison-Wesley Professional, 1995.

This is a lovely history of the ARPANET as it grew into the Internet, written by a historian who has been hanging out with UNIX people long enough to sound like one of them!

- COMER, DOUGLAS. *Internetworking with TCP/IP Volume 1: Principles, Protocols, and Architectures* (5th Edition). Upper Saddle River, NJ: Prentice Hall, 2006.

Doug Comer's *Internetworking with TCP/IP* series was for a long time the standard reference for the TCP/IP protocols. The books are designed as undergraduate textbooks and are a good introductory source of background material.

- HUNT, CRAIG. *TCP/IP Network Administration* (3rd Edition). Sebastopol, CA: O'Reilly Media, 2002.

Like other books in the nutshell series, this book is directed at administrators of UNIX systems. Half the book is about TCP/IP, and the rest deals with higher-level UNIX facilities such as email and remote login.

- FARREL, ADRIAN. *The Internet and Its Protocols: A Comparative Approach*. San Francisco, CA: Morgan Kaufmann Publishers, 2004.

- KOZIERAK, CHARLES M. *The TCP/IP Guide: A Comprehensive, Illustrated Internet Protocols Reference*. San Francisco, CA: No Starch Press, 2005.

An excellent collection of documents about the history of the Internet and its various technologies can be found at isoc.org/internet/history.

## 14.17 EXERCISES

E14.1 How could listening to (i.e., obeying) ICMP redirects allow an unauthorized user to compromise the network?

E14.2 What is the MTU of a network link? What happens if the MTU for a given link is set too high? Too low?
