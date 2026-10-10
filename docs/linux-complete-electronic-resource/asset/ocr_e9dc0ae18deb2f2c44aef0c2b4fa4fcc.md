Check for signs of tampering on the case and computer area. Although many intruders clean traces of their presence out of logs, it’s a good idea to check through them all and note any discrepancy.

It is also a good idea to store log data at a secure location, such as a dedicated log server within your well-protected network. Once a machine has been compromised, log data becomes of little use as it most likely has also been modified by the intruder.

The syslog daemon can be configured to automatically send log data to a central syslog server, but this is typically sent in cleartext data, allowing an intruder to view data as it is being transferred. This may reveal information about your network that is not intended to be public. There are syslog daemons available that encrypt the data as it is being sent.

Also be aware that faking syslog messages is easy—with an exploit program having been published. Syslog even accepts net log entries claiming to come from the local host without indicating their true origin.

Some things to check for in your logs:

+   * Short or incomplete logs
+   * Logs containing strange timestamps
+   * Logs with incorrect permissions or ownership
+   * Records of reboots or restarting of services
+   * Missing logs
+   * su entries or logins from strange places

We discuss system log data in the section, “Keep Track of Your System Accounting Data.”

# LOCAL SECURITY

The next thing to take a look at is the security in your system against attacks from local users. Did we just say local users? Yes!

Getting access to a local user account is one of the first things that system intruders attempt while on their way to exploiting the root account. With lax local security, they can then “upgrade” their normal user access to root access using a variety of bugs and poorly set up local services. If you make sure your local security is tight, then the intruder will have another hurdle to jump.