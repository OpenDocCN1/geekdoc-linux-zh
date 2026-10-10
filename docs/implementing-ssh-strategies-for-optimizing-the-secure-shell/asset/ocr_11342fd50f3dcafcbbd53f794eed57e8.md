![](bbox=[0.11, 0.06, 0.82, 0.52])

Figure 8.4 Sniffer capturing an Rexec connection.

# Why Access via SSH Is Better

After learning about the insecurities of RSH, Rlogin, and Rexec, you should now understand why utilities such as SSH were developed and widely adopted. The use of RSH, Rlogin, and Rexec in any hostile environment, whether it be the Internet, an internal network, a DMZ environment, an extranet, or even a local network, will cause a lot of security issues for a given network. In order to protect against the basic flaws of the protocols mentioned previously, SSH should be used. While RSH, Rlogin, and Rexec provide mod-erately different functions, all three of the utilities’ primary functions is to pro-vide the execution of a command on a remote server, either through a local terminal session or a remote execution service. SSH can eliminate the need for all three of these utilities by providing the same, if not better, remote execution service or terminal sessions with an encrypted and secure connection. Unlike RSH, Rlogin, and Rexec, SSH is not a clear-text protocol, so if passive attackers were sniffing the network, they would not be able to gain or view any useful