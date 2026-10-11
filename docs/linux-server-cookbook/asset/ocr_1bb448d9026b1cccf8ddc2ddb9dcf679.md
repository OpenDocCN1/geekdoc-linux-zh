outside of the network through the internet. The main security related to networking is to use a Firewall on the Linux system. Even though the network would be protected by a network firewall, it is important to protect the systems with their own firewall to create double protection.

Historically, firewall configuration in Linux was a complicated task that required knowledge about $iptables$, a tool to maintain filter rules in the Linux kernel. Modern distributions include high-level tools to manage firewall rules, helping administrators and regular users to main firewall rules in an easy way.

Depending on the Linux distribution used, the default firewall tool will be different. Red Hat Enterprise Linux and derivatives, such as CentOS Stream or Rocky Linux, rely on the $Firewalld$ project as firewall management. Ubuntu distribution uses an $Uncomplicated\ Firewall\ (ufw)$ as the default configuration tool to ease firewall configuration.

The default backend for the firewall solutions in modern distributions is $nftables$, which replaces the traditional $iptables$. It is possible to use the command $nft$ to manage or list the rules configured in the system.

The following schematic $figure\ \underline{8.1}$ shows packet flows through Linux networking:

![](bbox=[0.15, 0.52, 0.86, 0.84])

Linux services implement their own security configuration. For example, the service $SSH$ allows to configure to not allow login with the administrator user $root$ or only allows the connection using $SSH\ public/private\ keys$. Another example is