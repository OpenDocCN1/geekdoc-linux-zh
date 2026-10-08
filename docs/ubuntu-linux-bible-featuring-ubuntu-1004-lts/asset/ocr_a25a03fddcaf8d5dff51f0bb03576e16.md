# Part III: Ubuntu for System Administrators

+   - smtpd_tls_session_cache_database: Identifies the organization and location of the SMTP server TLS session cache used by the tlsmgr daemon.
- smtp_tls_session_cache_database: Identifies the organization and location of the SMTP client TLS session cache used by the tlsmgr daemon.
- myhostname: Identifies the actual Internet hostname of this system. By default, this value is the value returned by hostname().
- alias_maps: Identifies the organization and full pathname of the aliases used for local mail delivery.
- alias_database: Identifies the organization and full pathname of the aliases used for local mail delivery, which is updated using the traditional aliases command. This is often the same file as that identified by the alias_maps parameter, but need not be.
- myorigin: Identifies the name of the host or domain that mail is assumed to come from and is sent to. On Ubuntu systems, it is the name of a file containing whatever is specified as the mail name when installing Postfix. This is suitable for single-domain installations, but insufficient for Postfix mail servers that support multiple domains.
- mydestination: A list of domains for which mail is delivered via local mail delivery. I specified ubuntu.hostname as the name of my host when I installed Postfix—in most cases, mail.domain-name (e.g., mail.vonhostname, in my case) would be the standard name to use for a mail server to keep your sysadmins and make it easy to locate/identify your domain's mail server.
- relayhost: If outgoing mail must be sent to another mail server for delivery, this identifies that mail server; otherwise, it is empty.
- networks: Identifies the networks or specific hosts from which this mail server will send mail. This information is specified in both IPv4 and IPv6 formats. In this case, the mail server will only send mail from the loopback network, which is a problem. This is discussed in the following section, "Identifying Trusted Hosts and Domains."
- mailbox_size_limit: Identifies the maximum size of any mailbox on the system. In this case, 0 means there is no limit.
- recipient_delimiter: Identifies the separator used internally by the Postfix server between usernames and addresses.
- inet_interfaces: Identifies the network interfaces on which the machine can receive mail. In this case, the Postfix server will listen on all network interfaces.
- html_directory: Identifies the location of HTML files that describe how to install and configure a Postfix server and various Postfix features.

A complete list of Postfix configuration parameters and possible values is available in the files section of the online reference information for the postfix command (man 5 postfixconf) or online locations such as www.postfix.org/postfixconf.html.