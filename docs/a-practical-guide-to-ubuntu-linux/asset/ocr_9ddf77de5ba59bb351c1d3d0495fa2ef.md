# 652 CHAPTER 17 CONFIGURING AND MONITORING A LAN

![](bbox=[0.277, 0.083, 0.723, 0.298])

Figure 17-7 The Cacti Installation Guide screen

# # THE CACTI POLLER

The Cacti poller is run by the /etc/cron.d/cacti crontab file. The */15 entry in this file cause cron to execute the script every five minutes. For more information refer to "Crontab Files" on page 206.

```
$ cat /etc/cron.d/cacti
MAILTO=root
*/5 * * * * www-data php /usr/share/cacti/site/poller.php >/dev/null 2>/var/log/cacti/poller-error.log
```

# # CONFIGURING CACTI

Point a Web browser on the machine running Cacti at localhost/cacti/install; Apache redirects the browser to the Cacti Installation page. Click Next.

Confirm the information on the Cacti Installation Guide screen (Figure 17-7) and click Next.

The next screen displays several file paths and information about which versions of Net-SNMP and RRDTool are installed. Review this information and click Finish.

Next Next displays the User Login screen. Log in with the username admin and password admin. Cacti forces you to change the password for the cacti data-user named admin. After you change the password, Cacti displays the Console screen (Figure 17-8). The name of the screen appears just below the Console tab at the upper-left corner of the screen.

# # BASIC CACTI ADMINISTRATION

By default, Cacti collects data from localhost (the system it is installed on). Once a few poller cycles have passed (approximately 15 minutes after you installed Cacti), Cacti will display this information. You must install snmpd on the local system if you want to monitor the local system (page 654).