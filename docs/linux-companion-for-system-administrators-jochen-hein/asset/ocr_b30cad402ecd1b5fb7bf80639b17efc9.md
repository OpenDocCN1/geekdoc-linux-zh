# 532 NETWORK ADMINISTRATION

counterpart, tcpspray uses the internal discard service of the inetd on the computer specified as the parameter. Alternatively, you can also use the echo port if you specify the option -e.

| Additional Information and Sources |
|---|---|
| Man pages: | tcpspray(1) |
| ftp server: | sunsite.unc.edu |
| ftp server: | /pub/linux/system/network/admin |
| File name: | tcpspray-1.la.tar.z |
| Size: | about 12 Kbytes |

# 24.2.3 Testing of TCP services

For testing a TCP service, you can use the telnet program. To do this, you must establish a connection directly to the required port, after which you can test the service directly. We suggest that you begin by trying telnet localhost smtp. If you know how this protocol works (this is defined in [rfc0821]) you can now test this service manually.

It is often possible to start a new version of a daemon under a different port and check it there before replacing the old version. If a system is already utilized by users, care should be taken that such changes are kept as far as possible to them.

Listing 24.7 shows an example of a simple test of a POP3 server. POP3 servers are used to give users access to their mailboxes from remote machines (people are now migrating to IMAP (Internet Message Access Protocol), but for the purpose of this example we stick to POP3). Please note that the password is transferred transparently (security-aware tunnel POP3 over an ssh connection). Sometimes you see messages that are incorrectly interpreted by ssh or indicate an error that is not correctly displayed by the client. And if all fails, you may work through the description of the protocol in the corresponding RFC.