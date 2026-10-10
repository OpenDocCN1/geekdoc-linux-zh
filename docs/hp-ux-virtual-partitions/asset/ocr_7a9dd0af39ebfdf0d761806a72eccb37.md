# System Startup and Shutdown Scripts

Let’s take a look at an example startup and shutdown file for an application loaded onto an HP-UX system that is widely used for Internet applications called Cold Fusion. Like many applications loaded on HP-UX systems, Cold Fusion installs startup and shutdown scripts as a standard part of the installation of the product.

As mentioned earlier, the script used as part of the startup and shutdown process is in /etc/init.d. In our case, the name of the program is /etc/init.d/coldfusion and is shown in the following listing:

```
```
# cat /sbin/init.d/coldfusion
#!/bin/sh
#
# Start the Cold Fusion servers
#
    _   .   .....
    "  "      "   "    "   "      .   .   .
    "   .  "   —  —"  .   .  .
    "   "  "   "   "   "   "   "   "

export CFHOME

#
# Start/stop processes for Cold Fusion
#

rval=0
case "$1" in

        start_msg)
                print "Starting ColdFusion Application Server"
                ;;
        stop_msg)
                print "Stopping ColdFusion Application Server"
                ;;
        'r'wal')
                #Start_check "on/off switch", to set CF_AUTOSTART, in config.d file.
                RCFILE=/etc/rc.config.d/coldfusion
                if [ -f $RCFILE ]; then
                        . $RCFILE
                else
                        print "Warning: $RCFILE defaults file missing."
                        print "Starting ColdFusion by default."
                        CF_AUTOSTART=1
                fi
        # Start CP if switch is on.
                if [ - "$CF_AUTOSTART" -eq 1 ]; then
                        if [ ! -x $CPBIN/start ]; then
                                rval=$?
                        else
                                print "Error: ColdFusion startup script $CPBIN/start missing."
                                print "      ColdFusion not started."
                                rval=1
                        fi
                else
                        print "Notice: ColdFusion startup disabled in $RCFILE"
                        rval=2
                fi
                fi;
```
```