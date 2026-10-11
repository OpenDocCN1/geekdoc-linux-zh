
## Configuring the Server Side

In this section we will document the command line options to sshd, the server-side daemon, and its configuration files.

Normally, sshd is invoked at boottime by a start-up script. The RPMs we've used creates the /etc/rc.d/init.d/sshd script and links it to appropriate kill and start scripts (see Start-Up Scripts on page 24 in Chapter 3 for an overview of the system scripts). By default, sshd listens to port 22. When a connection request comes in, sshd forks a child sshd that will handle all key exchanges, authentication, encryption, and data transfers for the specific connection. While it is possible to invoke sshd through inetd or xinetd (see Replacing inetd with xinetd on page 226 of Chapter 10 for a discussion of xinetd), it is not recommended because of the potential initial delays incurred by the RSA Host-Based Authentication mechanism (described in Host-Based Authentication Using RSA on page 257), which may cause premature connection refusals.

The sshd gets its configuration information first from the command line and then from the /etc/ssh/sshd_config configuration file. Command line options take precedence over settings in /etc/ssh/sshd_config. Table 11.4 describes the available command line options to sshd.

The keywords or parameters and their meanings in the /etc/ssh/sshd_config file are described in Table 11.5. All blank lines and lines beginning with # in this file are ignored. All keywords are case insensitive, and a space separates the keyword from its arguments.

### Table 11.4 Command Line Options to sshd

| Option | Description |
| :--- | :--- |
| -b bits | Specifies the number of bits in the Server Keys. Default is 768 bits. |
| -d | Debug mode. The daemon generates debug output to syslog. In this mode sshd will not fork subprocesses and will terminate itself upon disconnection. |
| -t config_file | Specifies the absolutely qualified name of the sshd configuration file. The compiled default for the RPMs discussed herein is /etc/ssh/sshd_config; ordinarily it is /etc/ssh/sshd_config. |
| -g grace_time | Sets the time, in seconds, for clients to authenticate the user. If the user authentication process does not complete prior to this time, then the server will disconnect and exit. The default is 600 seconds (normally, more than sufficient). A value of 0 indicates no limit. |
| -h host_key_file | Specifies the absolutely qualified name of the file containing the Private Host Key. The compiled default for the RPMs discussed herein is /etc/ssh/ssh_host_key; ordinarily it is /etc/ssh/ssh_host_key. |
| -i | Indicates that sshd is invoked through inetd (or xinetd). Due to authentication delays, particularly if sshd needs to generate new Server Keys, this is not recommended as it may cause premature disconnects. |
| -k key_gen_time | Specifies in seconds how frequently sshd regenerates the Server Keys after its first use. Default is 3600 seconds. A value of 0 causes these keys to never be regenerated and cannot be recommended. Since these keys are never stored anywhere, it is nearly impossible to recover the key after the specified time period. This makes cryptographic attacks much more difficult as long as the keys are changed frequently. |
| -p port | Specifies the port that sshd listens to for incoming requests. The default is 22. |
| -q | Quiet mode. This suppresses all logging except fatal errors. Normally, the initial connection request, authentication information, and connection termination are logged through the syslog facility daemon. See the syslogFacility keyword in Table 11.5 for configuration options. |
| -V | Specifies SSH Version 2 compatibility mode. This option should be used in environments where both versions 1.x and 2.x are running. |

### Table 11.5 Keywords in /etc/ssh/sshd_config

| Keyword | Description |
| :--- | :--- |
| AllowGroups | This keyword may be followed by a space-separated list of group names. If so specified, only users whose primary group appears in this list will be allowed to log in. This specification is in addition to all other authentication requirements. By default, no group checking is done. Group names may include the * and ? wildcards, which have the same behavior as in the shell. |
| DenyGroups | Same as AllowGroups, except that users whose primary groups are listed will be denied access. By default, no groups are denied. |
| AllowHosts | This keyword may be followed by a space-separated list of hostnames or IP addresses. If specified, logins are allowed only from the indicated hosts. The * and ? wildcards may be used. Aliased hostnames will not match, so be sure to use canonical hostnames. Note that, if TCP_wrappers support is compiled in, the intersection of this list and the rules in /etc/hosts.allow applies. See *TCP Wrappers* on page 194 in Chapter 10 for a discussion of TCP_wrappers. |
| DenyHosts | Same as AllowHosts, except that it denies access requests from the listed hosts. If TCP_wrappers support is compiled in, the intersection of this list and the rules in /etc/hosts.deny applies. |
| AllowHosts | This keyword may be followed by a space-separated list of hostnames or IP addresses. The * and ? wildcards may be used. If specified, trusted hosts ($HOME/.rhosts, /etc/hosts.equiv, $HOME/.shosts, and /etc/shosts.equiv) entries are honored only for the indicated hosts. By default, all hosts may be in a trusted host file. For this to have any effect one or both of the keywords RhostAuthentication and RhostRSAAuthentication must be set to yes. |
| DenyHosts | Same as AllowHosts, except that the indicated hosts will not be afforded trusted host status. |
| AllowUsers | This keyword may be followed by a space-separated list of usernames or username@hostName patterns. The hostname may be either the hostname or IP address. The * and ? wildcards may be used. If specified, only the indicated users (from the indicated hosts, if specified) will gain access. This specification is in addition to all other authentication requirements. By default, all users are allowed. |
| DenyUsers | Same as AllowUsers except that any entries in the list are denied access. |
| AccountExpireWarningDays | Specifies the number of days prior to the expiration of a user account that sshd will display a warning to the user. The default is 14; if set to 0, warning messages are disabled. Note that these messages are in addition to any generated by PAM or other mechanisms. |
| AllowTCPForwarding | If yes, port forwarding requests by the client are honored. If no, they are not. |
| CheckMail | If yes, sshd will print a message about mail. If no, it will not. The default is yes. This will duplicate messages generated by pam_mail, if that PAM module is used. |
| FascistLogging | If yes, sshd logs verbosely and includes detailed information about the authentication dialog that is useful for debugging (and may also give an interloper some additional information about the configuration of the environment). The default is no, which should be the setting except for debugging. |
| ForcedEmptyPwdChange | If yes, sshd will force a password change. By default this parameter is no, letting PAM take care of these issues. |
| ForcedPwdChange | If yes, sshd will force the user to change his or her password if it has expired. By default this parameter is no, letting PAM take care of these issues. |
| HostKey | Specifies the file containing the Private Host Key. Default is /etc/ssh_host_key. Set to /etc/ssh/ssh_host_key in the RPMs. |
| IdleTimeout | If the connection has been idle for the indicated amount of time, the connection is closed. The time may be specified in *seconds, minutes, hours, days*, or *weeks*, where *seconds, minutes, hours, days*, and *weeks* are positive integers. |
| IgnoreRhosts | If *yes*, all *$HOME/.rhosts* and *$HOME/.shosts* are ignored. The */etc/hosts.equiv* and */etc/shosts.equiv* files are unaffected by this keyword. The default is *no*. |
| IgnoreRootRhosts | Same as *IgnoreRhosts* except that it applies only to *root*. It defaults to the value of *IgnoreRhosts*. |
| KeepAlive | If *yes* (the default), *sshd* will check connectivity to the client periodically. If connectivity cannot be verified, *sshd* closes the connection. This is true even if the verification fails due to a temporary routing problem. To disable this mechanism, you must set this keyword to *no* in */etc/ssh/sshd_config* and */etc/ssh/ssh_config* or *$HOME/.ssh/config*. |
| KeyRegenerationInterval | Specifies the time in seconds to regenerate the Server Keys after their first use. The default is *3600*. The value *0* means that the key will never be regenerated. The *-X* command line option overrides this keyword; see Table 11.4 on page 269. |
| ListenAddress | Specifies the interface to which *sshd* binds. Normally, this is set to *0.0.0.0*, meaning any interface. This is useful on systems with multiple interfaces where you wish to limit incoming *ssh* connections to a specific interface. The value of this keyword must be an IP address of a local interface. |
| LoginGraceTime | Sets the time, in seconds, for clients to authenticate the user. If the user authentication process does not complete prior to this time, then the server will disconnect and exit. The default is *60* seconds (normally, more than sufficient). A value of *0* indicates no limit. This value is overridden by the *-G* command line option; see Table 11.4 on page 269. |
| PasswordAuthentication | If *yes* (the default), then, if other nonpassword authentication mechanisms fail, the user is prompted for a password which is verified internally by *sshd*. Setting this keyword to *no* disables password authentication altogether. |
| PasswordExpireWarningDays | Specifies the number of days prior to the expiration of a password that *sshd* will display a warning to the user. The default is *14*; if set to *0*, warning messages are disabled. Note that these messages are in addition to any generated by PAM or other mechanisms. |
