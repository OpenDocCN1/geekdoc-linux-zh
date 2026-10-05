critical security patch. This can also be used to execute monitoring scripts that enable the administrator to do preventive work, for example, to clear a temporary directory before a file fills ups.

# Remote support

Almost all on the client can be provided by accessing the client from a remote location. The only types of problems that still require hands-on interaction at the client are network problems. All other problems reported by the user can be handled by logging into the client remotely and studying the system configuration and the log files. This capability could improve the effectiveness of helpdesk staff significantly.

# Remote management and provisioning tools

There are a lot of tools available in the open source community as well as from commercial parties for remote management or monitoring and provisioning. Some of the most popular tools are:

+   * Webmin⁶
* Big Brother/Big Sister⁷
* Nagios⁸

Webmin is mainly used for remote management of a single machine. Big Brother and Nagios are mostly used to monitor run-time properties of a network of machines, then to apply administrative tasks when system properties go outside of established limits.

Commercial tools are available for these tasks as well. For example, IBM provides Tivoli Configuration Manager and Tivoli Monitoring for automation of monitoring and remote management tasks.

Red Hat Linux distributions can use the Red Hat Network (RHN) to remotely manage individual systems or groups of systems. The RHN also offers automatic provisioning services as described in "Administration of Red Hat Desktop" on page 91.

Novell Linux Desktop distributions use ZENWorks software to remotely manage or provision systems, as described in "Administration of Novell Linux Desktop" on page 93. After Novell acquired Ximian, the SUSE Linux distributions adopted Ximing's Red Carpet product (now under the ZENWorks name) as the standard tool for their enterprise distributions. Before

```
⁶ http://www.sourceforge.net/projects/webadmin; http://www.webmin.com
⁷ http://www.sourceforge.net/projects/big-brother;
://www.sourceforge.net/projects/bigsister; http://www.b4.org
⁸ http://www.sourceforge.net/projects/nagios; http://www.nagios.org/
```