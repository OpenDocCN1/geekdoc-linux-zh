`[ramon]$ rpm -q tcp_wrappers`  
`tcp_wrappers-7.6-10`

Listing 4.7 shows a system that was running version `7.6.7` and has been upgraded to the more recent version `7.6.10`.

> **WARNING** Trojan horse versions of TCP Wrappers were placed on a number of public FTP servers around January 21, 1999. The offending file was labeled as version `7.6`, and it introduced a root vulnerability on the systems where it was installed. I strongly discourage you from downloading this file (the tar archive was named `tcp_wrappers_7.6.tar.gz`). Obtain it in RPM format from a well-known and trusted repository instead. Refer to CERT Advisory `CA-1999-01` for more detailed information.

Once you have verified your TCP Wrappers installation, it’s time to look at the configuration files that you need to edit. This is the topic of the next section.

# # Configuring TCP Wrappers

The first step in configuring the TCP Wrappers package is to make sure it is being properly invoked. This is done by ensuring that the **service** name field in `/etc/inetd.conf` is set to the location of the `tcpd` binary (`/usr/sbin/tcpd` in Listing 4.2). This allows the TCP Wrappers daemon to intercept all incoming requests and to examine them before passing them on to the real server application. The name of this application is specified in the **server program arguments** field of `/etc/inetd.conf`.

The real power of the TCP Wrappers tool is the fine-grain level of access control that it provides. The system administrator can define a set of allowable clients for each network service. To do this, you must edit two configuration files that are typically found in the `/etc` directory: `/etc/hosts.allow` and `/etc/hosts.deny`. These files are already included in most Linux distributions, but make sure that they exist and edit them to reflect your site’s security policy.

These two files are consulted by the TCP Wrappers application in that order (first `hosts.allow`, then `hosts.deny`) and can contain rules specifying access-control directives. The connection request is granted unless there is a specific `deny` directive found in one of these files. I recommend that your `/etc/hosts.deny` file have a catchall rule at the end that denies all requests. This forces you to have to enter specific `allow` directives for those services that should be permitted.

The basic syntax for the rules in the `/etc/hosts.allow` and `/etc/hosts.deny` files is as follows:

`daemon_list : client_list [ : shell_command ]`