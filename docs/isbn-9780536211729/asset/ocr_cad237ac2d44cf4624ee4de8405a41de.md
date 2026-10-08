dle the initial three-way handshaking for TCP, this method will not detect TCP scans or various other stealth scans, such as the FIN, Null, or Xmas scans.

Stealth scan mode (-stcp or -udp). PortSentry will open a raw socket to listen in Promiscuous mode and trigger if any port within the specified range that not already have a connection listening on it is attacked. Stealth scans will be detected.

Advanced stealth scan mode (-atcp or -udp). PortSentry will open a raw socket to listen and trigger if any port within the specified range that not already have a connection listening on it is attacked. Stealth scans will be detected. The advantage of the advanced stealth scan mode over the previous mode is that it will detect crackers client-side random high port numbers that might open, in the hope of hijacking existing connections. It is also very sensitive, some might call it a trigger if a suitably large range of ports is specified. Another advantage is that crackers will see the port as closed or filtered, not open as would be the case with Basic TCP mode.

The downside is that it allows a cracker to do a DoS attack by spoofing a source address. While PortSentry's limited documentation experience expresses great concern about this, unless you are a very well-known site, this is a very unlikely prospect. It may happen unintentionally to internal users on occasions (every few months) but this requires only restarting PortSentry.

Most SysAdmins find advanced stealth mode to be most suitable and will want to run both a TCP and a UDP version. It will detect connect(), SYN (half open), FIN, XMAS, NULL, any TCP scan, and all UDP scans, except small fragments. (Firewall should be configured to defrag all packets to protect against fragmentation attacks, as discussed in "Fragmentation Attacks" on page 567). The two stealth modes are available only on Linux at this time, according to the documentation.

PortSentry will notify you of any attack using the syslog facility; this assumes you will see the log in a timely manner, notice the problem, and react. Psionic's Logcheck (now LogSentry) program works for your purpose, with the limitation that it may be invoked manually every hour or so and can have false positives. It was covered in "Using Logging to Check Files You Never Check" on page 346. An alternative is to use PortSentry's KILL_RUN_CMD capability to let it send you e-mail immediately upon detecting an attack. PortSentry also offers the very valuable Firewall capability by interfacing with IP Tables, IP Chains, TCP Wrappers, or by invoking any user-specified command in KILL_RUN_CMD. This can be used to interface with the Cracker Trap.

Normally, when running on a firewall, PortSentry will detect only attacks against the firewall itself or broadcast destinations that include the firewall. However, port redirection may be used on the firewall to redirect packets for the monitored ports on other systems back to the firewall allow PortSentry to react.

The latest version of PortSentry may be downloaded from Psionic's Web site:

www.psionic.com/abacus/portsentry/