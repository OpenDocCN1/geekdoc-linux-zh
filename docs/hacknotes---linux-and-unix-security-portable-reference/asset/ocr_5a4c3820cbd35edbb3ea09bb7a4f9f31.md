# Chapter 12: Hacking with the Sharp Zaurus PDA 185

Nessus server. Please see Chapters 4 and 11 for more information on the Nessus scanner.

The zNessus client requires that the Nessus server be configured to support unencrypted communication (which is disabled by default). If you decide to disable encryption on your Nessus server, be sure to block all incoming traffic to the Nessus port (1241 by default). Use the OpenSSH client to connect to your Nessus server host in order to tunnel your zNessus traffic securely.

# MTR

MTR (Matt's TraceRoute, in the next illustration) is a tool that combines the functionality of the ping and traceroute programs into a single program. (Please see Chapter 2 for more information on ping and traceroute.) The binary package for the MTR port for Zaurus can be downloaded from http://psifertex.com/zaurus/mtr_0.51_arm.ipk.

![](bbox=[0.297, 0.415, 0.672, 0.727])

# DIG

The dig tool can be used to interrogate DNS servers in order to fetch information such as MX records and server version information, as well as perform other DNS lookup queries. Dig for Zaurus is available at http://killefiz.de/zaurus/showdetail.php?app=362.