# # Keeping Up Performance

With respect to keeping your performance where you want it, make sure each Slackware system runs no more than one CPU-intensive application (such as a database, firewall, or mailserver) at a time. Keeping your Slackware systems relatively uncomplicated also makes them less vulnerable and troubleshooting a lot easier. When a server has one specific role, you can simplify – turn down many of the other services that usually run by default. For example, an SMTP server doesn't necessarily need the X-Window system running, or many of the Inetd services, and certainly not an HTTP server.

Careful scrutiny of server roles can boost not only performance, but security as well. Turning off unwarranted network services can plug some security holes – for example, do you really need to rlogin to the SMTP server? Do you need a mail server to be CGI-enabled on its seldom-used HTTP server? If not, consider what you can safely turn off.

A large company may have many servers for different purposes; if you're running a small network in your home or for a small company, you may not want or need as many. You might, for example, want no more than three – a database, a DNS server, and a firewall. You could try running the DNS server directly on the firewall, but if you do, at least run the database on a separate system. A database eat lots of CPU time; also, if you keep it off the firewall you can enhance security: someone who breaks into your firewall hasn't immediately broken into your data as well.

# # Keeping Your Data Safe

When you've got your critical data up and running, your next step is to ensure its safety. This includes locking backups in a safe, setting the proper permissions on critical files, and creating only the necessary user accounts.

# ## WHICH USER ACCOUNTS ARE REALLY NECESSARY?

Often a particular server process has to run as a certain user to manage access and prevent unauthorized use of its functionality.

These docile accounts are created often for HTTP servers (such as Apache) and for other daemon processes. By default, the nobody account is used for daemons, but you may need to differentiate and create your own. (A good one for an HTTP server, for example, would be webuser.) Remember: you can disable actual logins and home directories on these user accounts. Further, you can allow processes to execute only under their own IDs, without actually gaining access to the system through telnet, or by some other unintended method.

![](bbox=[0.16, 0.9, 0.24, 0.96])

See Chapter 8 for more information on locking an account.This can help prevent unwarranted exploits against your server.