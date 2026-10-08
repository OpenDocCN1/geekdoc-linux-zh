# 2.10 Turn Off Unneeded Services

The listed services are the ones with daemons that are started when the system comes up. On a Red Hat-derived system, there is a menu-driven program that may be used to see and change which of these services are started. To invoke the program issue the command

ntsysv

# 3. Inspect /etc/xinetd.d/* or /etc/inetd.conf

/etc/xinetd.d directory contains a configuration file for each service that will be provided by xinetd, the new superserver. While managing many configuration files is more effort than the single configuration file of inetd, xinetd has many capabilities suitable for heavy-duty servers. These include limiting the number of simultaneously running instances of a particular service and altering each server's process priority from the default. It has the libwrap library built in to parse the /etc/hosts.allow and hosts.deny files to decide which remote systems are allowed to use each service. By using libwrap, the system load is substantially reduced by eliminating the need to fork the tcpd process to do this.

Some of the more useful variables that may be used in a configuration file for a service are

+   - disable
  Disables a service without removing the configuration file.

+   - instances
  Specifies the number of simultaneous instances of a service that are allowed or UNLIMITED to not enforce a limit.

+   - nice
  Increases the niceness (i.e., lowers the server's priority) or vice versa.

+   - user
  Specifies what user permissions the server will run under.

+   - group
  Specifies what group permissions the server will run under.

+   - SENSOR
  Listens on this port for attackers, but does not actually start a server when someconnects. Instead, does not accept further connections from the client system until the deny_time setting expires. This can slow down crackers but is less effective than a good Adaptive Firewall.

+   - only_from
  Specifies what hosts are allowed to use this service. It is redundant with respect to TCP Wrappers that it supports IPv6 addresses. The move to IPv6 seems almost slow as the move in the U.S. to the metric system

+   - access_times
  Specifies what times of the day the service will be supported. If you manage a 9-to-5 operation, access_times can be used to prevent people from trying to bruteforce crack passwords at night by hitting your SSH, FTP, POP, or IMAP servers. Unfortunately, one cannot specify days of the week, so crackers still can attack you during the day on weekends. It can also be used to limit public services and the requisite load during the day.