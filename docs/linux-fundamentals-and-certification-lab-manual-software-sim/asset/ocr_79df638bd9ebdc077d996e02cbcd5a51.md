![](bbox=[0.84, 0.08, 0.97, 0.11])

The CUPS HTTP server can be reached on the local machine by using the URL http://127.0.0.1:631/admin. When asked for the administrator ID and password, use root or some other superuser account. The default CUPS configuration limits administration to the local machine. To open up access, edit the /etc/cups/cupsd.conf file and comment out the lines reading:

```
Order deny,allow
Deny from all
Allow from 127.0.0.1
```

# FIGURE 9-12  CUPS HTTP administration.

![](bbox=[0.3, 0.34, 0.87, 0.66])

CUPS is an extensible printing system and represents a leap forward for Unix/Linux print systems. The IPP protocol is a client/server protocol that allows the server side to be either a separate print server or a printer with embedded networking capabilities. CUPS supports legacy programs and can easily handle LPD requests and other requests.

Objective 3.6

# Configuring a Printer

Several applications can be used to configure a printer. The setup program in many Linux distributions allows users to configure a printer. Many distributions have their own printer configuration tools as well. Regardless of the tool used to configure the printer, most installations use either LPng or CUPS. Currently, many major Linux distributors recommend using CUPS. CUPS is the default on SuSE, Mandrake, Red Hat, and other Linux distributions. This section will outline the usage of printconf, a printer setup program available in Red Hat version 9. Both text and GUI versions will be used. The text version will add a local printer and will be demonstrated first.