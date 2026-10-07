# Basic lpd Functionality

A master line printer daemon runs constantly to keep track of any print spooling needs on the system. The master lpd is started at boot time in the same way as other daemons we discussed when we talked about system initialization. Red Hat Linux has an lpd script in /etc/rc.init.d, which runs at boot time. You can start or stop LPRng at other times by issuing a command consisting of the full path to the lpd script, a space, and one of the following: start, stop, status, or restart. When the line printer daemon is started, it reads the /etc/printcap file, discussed earlier. Listing 13.1 shows an example of a printcap file.

+   Listing 13.1 An Example printcap File

```
1p|1p0|lexmark:\n:sd=/var/spool/lpd/lexmark:\n:mx#0:\n:sh:\
:lp=/dev/1lp0:\n:if=/var/spool/lpd/lexmark/filter:\nlp1|hp4000:\n:sd=/var/spool/lpd/hp4000:\n:mx#0:\n:sh:\
:rm=-tennessee:\n:rp=hp4000:\n:if=/var/spool/lpd/hp4000/filter:\nlp2|epson:\n:sd=/var/spool/lpd/epson:\n:mx#0:\n:sh:\
:if=/var/spool/lpd/epson/filter:\n:af=/var/spool/lpd/epson/acct:\n:lp=/dev/null:
```