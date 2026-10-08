# RELIABILITY OF NAME SERVERS 421

Advisories on http://www.cert.org or http://ftp.cert.org/pub/cert_advisories.

One widespread type of attack is the faking of name server responses. Many programs (for example login) admit users or access in dependence on the computer name. In an incoming connection, however, only the IP address of the sender is available, if this has not already been falsified by IP spoofing. Thus, for authentication, a reverse lookup is carried out which is processed by the responsible name server.

Since the responsible name server might be under the control of the attacker, any falsification is possible. Defence measures consist of improved programs that countercheck DNS responses a second time, new protocols (for example ssh instead of rsh), and not using any vulnerable services.

The use of a DNS is also very useful in the intranet, because it is relatively laborious to maintain the host tables on all computers. Here, the advantage of the DNS is that there is an ultimate instance whose data is available everywhere. Alternatively, in a UNIX network, you can also use the NIS to distribute the host tables, but only to UNIX systems.