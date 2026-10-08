A better solution would be to have some conditional code in the firewall script that is keyed to the time of day and day of the week and to invoke this script at the start and end of the business day from cron.

Not all Linux distributions have moved to xinetd, due to concerns about security bugs and its configuration files requiring more effort to maintain. Additionally, there is not an overwhelming advantage over inetd. Unlike xinetd, the inetd program uses the /etc/inetd.conf text file to list all of the ports that it will listen on, then it forks the appropriate program to process the request. Red Hat's inetconvert for configuring one's inetd.conf to configuration files suitable for xinetd was discussed in “Revving Up Red Hat 7.3” on page 60.

# 4. Use ps to list processes

The ps (Process Status) command may be used to list all running processes on the system and recognize that those are daemons. This requires a fair amount of system knowledge. Many daemons have names that end in “d” (for daemon). The following invocation of ps is typical.

```
ps -axlw
```

A flag causes the listing of all processes, not just those on the invoker's terminal. The x flag indicates that processes not associated with a terminal should be listed. typically are invoked during system setup or via cron. The l flag indicates a long listing.
The w indicates wide; the output will be truncated at 130–160 columns instead of 80, depending on the Linux distribution and version. The second w indicates wider; the output will be unlimited on Red Hat. On Slackware, each w adds another 80 columns of possible outputnThe suggested rules for deciding which services to allow are as follows:

+   A. Do not run any service that you do not understand. It is easier to turn them off than it is to recover from an intrusion and violated confidentiality.

+   If you do not understand it, you cannot understand the security implications. If you do not understand the security, you might not have any security.

+   B. Consider the choice of leaving a service on, risking reduced security, versus-turning the service off and “breaking something.” Pick better security and turn it off.

+   C. UDP source addresses can be faded, so services that rely on UDP source addresses for security are not secure (unless you absolutely trust every system that can “get to” the clients and servers using UDP).

+   If the systems on your LAN can be trusted, and your UDP services will talk only to IP addresses on your LAN, and your firewall will block systems