
# PART 2 Layered Security and Linux

But that's also a weakness, since the nmap command can detect the services running on obscure ports.

# Obscurity by Other Means

The use of nonstandard open ports is just one way to obscure local systems and networks. Services can be obscured by their login messages. Services can also be obscured by their error messages. While Chapter 8 covers the Secure Shell (SSH), the following directive in the main configuration file (/etc/ssh/sshd_config) points to the /etc/issue.net file as the login message for users:

`Banner /etc/issue.net`

Once configured, you can add appropriate legal warnings or other messages that may mislead a black-hat hacker. The file is associated with login messages to Telnet, which you choose to take the risks associated with that protocol, which transmits sensitive information in clear text. For that reason and others, the use of Telnet is not recommended.

As for errors, the information shown when a user navigates to a non-existent Web page can also be important. If you're using the Apache Web server, that information depends on the ServerTokens directive in the associated configuration file. Full information leads to the following message when a user tries to navigate to a nonexistent Web page:

- Apache/2.0.63 (Unix) OpenSSL/0.9.8e/0.9.8e-fips-rhel5
- JRUN/4.0 mod_auth_paththrough/2.1 mod_bwlwimited/1.4
- FrontPage/5.0.2.2635 Server at example.com Port 80

That's a lot of information a black-hat hacker may be able to use. Assuming the noted Web server actually includes the noted versions of the listed software, black-hat hacker should be able to check for known flaws in each of those systems.

If Apache were configured with a less informative setting, the user would see the following information instead:

`Apache Server at example.com Port 80`

That's a lot less information for a black-hat hacker. In other words, obscurity can make it more difficult for a black-hat hacker to break into your systems.

# Protect with TCP Wrappers

The TCP Wrappers system was originally developed to protect the services controlled through the internet server and extended internet server services described in Chapter 6. It's extended statically and dynamically to additional services as will be described shortly. You'll see how such services can be protected through /etc/hosts.allow and /etc/hosts.deny configuration files.

# CHAPTER 7 | Networks, Firewalls, and More

# What Services Are TCP Wrapped?

As mentioned, there are several groups of services that may be protected by TCP Wrappers. If you're looking for candidate services, examine the following configuration files and commands:

- Regular internet super server—Any services configured in the /etc/inetd.conf file can be protected by TCP Wrappers, as long as the TCP daemon (/usr/sbin/tcpd) is included in the server column of the associated configuration directive.
- Extended internet super server—Any services configured in the /etc/xinetd.conf file can be protected by TCP Wrappers. Normally, the /etc/xinetd.conf file points to individual services in the /etc/xinetd/ directory.
- Services dynamically linked to libwrap.so.—Run the command on the full path to a target daemon, such as the SSH service at /usr/sbin/sshd. If you see a libwrap file in the output, there's a dynamic noted service and TCP Wrappers.
- Services statically linked to libwrap.so.—Run the strings command on the full path to a target daemon, such as the Portmap at /sbin/portmap. If you see a libwrap or /etc/hosts.allow file in the output, there's a static link between the noted service and TCP Wrappers.

All services can be protected with appropriate directives in the /etc/hosts.allow and /etc/hosts.deny configuration files.

# Configure TCP Wrapper Protection

Any services that have the protection of TCP Wrappers are filtered through rules configured in /etc/hosts.allow and /etc/hosts.deny files. Rules in these files may be configured by Internet Protocol (IP) address, domain, or user. Because rules in these files may conflict, they are considered in the following order:

- /etc/hosts.allow—Rules in this file are first checked. If the service is explicitly allowed, control is returned to the service. Any rule in /etc/hosts.deny are ignored.
- /etc/hosts.deny—Any service that it beyond /etc/hosts.allow looks at rules in this file that explicitly denies access to a service is considered. These rules may send a message to the client.
- If no rule applies—if no rule is configured in either file, access is granted.

Directives in both configuration files may be set up with the following format:

```
daemons : clients { : command }
```

One way to set up maximum protection with TCP Wrappers is to include the following rule in the /etc/hosts.deny file. It denies access to all daemons from all clients:

```
ALL : ALL
```

# PART 2 | Layered Security and Linux

You can configure other rules in /etc/hosts.allow to explicitly allow access to desired services. First, confirm that the SSH service is associated with TCP Wrappers with the following command:

```
$ /usr/sbin/sshd | grep libwrap
```

Once the status of SSH and TCP Wrappers is confirmed, you can allow access to SSH with the following command.
