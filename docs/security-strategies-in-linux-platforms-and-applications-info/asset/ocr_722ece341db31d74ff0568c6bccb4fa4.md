# Default Rsyslog Configuration

While the strength of Rsyslog comes from a remote server, remote least transmission of logging information is disabled by default. Generally, you should install at least the rsyslog and tunnel packages on client and server systems. If you want encryption, two basic choices are available in separate packages, based on Transport Layer Security (TLS) and the Generic Security Services Programming Interface (GSSAPI). On Red Hat and Ubuntu systems, these options are available in the rsyslog-gssapi packages, respectively.

The rsyslog service starts by a central configuration file, rsyslog. The location of that file varies by distribution. On Red Hat systems, it's in the /etc/sysconfig/default directory.

Depending on the release, the applicable variable in the rsyslog file is either RSYLOG_OPTIONS or SYSLOG_OPTIONS. To some extent, the name of the variable doesn't matter, as both are given as options to the Rsyslog daemon when it starts. If you want to use compatibility-mode options, substitute the -c 2 option on Red Hat systems or -c o on Ubuntu systems for the value of the aforementioned variable.

# The Standard Rsyslog Configuration File

The Rsyslog configuration file is normally divided into three sections: modules, directives, and rules, which normally incorporates the basic rules described earlier for the /etc/syslog.conf file. As described at http://www.rsyslog.com/doc-rsyslog_conf_modules .html, modules fall into a number of categories. Global directives set parameters such as timestamps and periods.

# Rsyslog Modules

Modules with the Rsyslog service can be configured in a number of areas. First, the default modules are straightforward, as they enable local system and kernel logging:

```
$ModLoad imuxsock
$ModLoad imk log
```

Two additional modules are available in comments, based on either the User Datagram Protocol (UDP) or the Transport Control Protocol (TCP). Port 514 is the default for the system logging service. If you've replaced it with Rsyslog, that port would be:

```
$ModLoad imudp
$UDPServerRun 514
```

If you want to set up the local system as a Rsyslog-based logging server, you'd want to enable these two directives, as TCP communication is required for encrypted transmission of log files:

```
$ModLoad imtcp
$InputTCPServerRun 514
```

![](bbox=[0.933, 0.203, 0.966, 0.355])