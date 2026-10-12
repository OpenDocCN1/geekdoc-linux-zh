+   KILL_RUN_CMD: Instead of using firewalls, rerouting, or TCP wrappers to deny an intruding computer from accessing your computer, you can choose any command you like in response. With the BLOCK_TCP and BLOCK_UDP options set to “2”, the value of KILL_RUN_CMD is run in response to a scan of your monitored ports.
+   
+   The value of KILL_RUN_CMD should be the full path to the script you want to run, plus any options. To include the IP address of the remote computer or the port number that was scanned, you could include the $TARGET$ or $PORT$ variables, respectively. Here is how the example appears that you would want to modify:
+   
+   KILL_RUN_CMD="/some/path/here/script $TARGET$ $PORT$"

> **CAUTION**: Do not use any KILL_RUN_CMD to retaliate against the intruding remote host. Firstly, it is quite possible that the computer that is scanning your ports has itself been cracked and is thus not a valid target for retaliations, and secondly, retaliation may simply incite the cracker into further attacks on you.

+   PORT_BANNER: You can send a message to the person who sets off the PortSentry monitor by setting the PORT_BANNER option. By default, no message is defined. However, you can uncomment the following line to use that message. (An abusive message is not recommended.)
+   
+   PORT_BANNER="** UNAUTHORIZED ACCESS PROHIBITED *** YOUR CONNECTION ATTEMPT HAS BEEN LOGGED. GO AWAY."

The number of scans from an intruding computer that PortSentry will accept before setting off the responses described above can be set by using the SCAN_TRIGGER option. By default, that option is set as follows:

SCAN_TRIGGER="0"

The “0” value means that you won’t accept any scans from an intruding system. In other words, the first scan will trip the PortSentry monitor. You can increase this value to be tolerant of one or more errant scans (though you probably won’t want to).

# Changing the portsentry.modes file

The /etc/portsentry/portsentry.modes file defines the modes in which the PortSentry command is run at boot time. Here is how that file appears by default:

```
tcp
udp
#stcp
#sudp
#atcp
#audp
```

The tcp and udp options are the basic PortSentry modes for the TCP and UDP services, respectively. Your other choices of options include stealth TCP (stcp) and advanced stealth