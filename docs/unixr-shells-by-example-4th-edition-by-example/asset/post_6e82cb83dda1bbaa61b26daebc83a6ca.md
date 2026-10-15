
## EXPLANATION (CONTINUED)

4 The script is run again, this time starting the cron daemon.

5 The script is run a third time. This time the daemon will be stopped, then started again.

Below is a simplified version of the boot script for the cron daemon from Red Hat Linux. This script sources another script called functions, which defines daemon and killproc for the script. The daemon function takes a daemon name as an argument. It attempts to start that daemon and will return a success or failure code depending on what happened.

### EXAMPLE 16.14

```
#!/bin/bash
# crond Start/Stop the cron clock daemon.
#
# chkconfig: 2345 90 60
# description: cron is a standard UNIX program that runs
# user-specified programs at periodic scheduled times.
# config: /etc/crontab
# pidfile: /var/run/crond.pid

# Source function library.
. /etc/init.d/functions
RETVAL=0
# prog="crond"
start() {
 echo -n "$prog: Starting $prog: "
 daemon crond
 RETVAL=$?
 echo
 [ $RETVAL -eq 0 ] && touch /var/lock/subsys/crond
 return RETVAL
}
stop() {
 echo -n "$prog: Stopping $prog: "
 killproc crond
 RETVAL=$?
 echo
 [ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/crond
 return RETVAL
}
restart() { stop ; start }
case "$1" in
 start) start ;;
 stop) stop ;;
```

```
restart) restart ;;
*)    echo $'Usage: $0 {start|stop|restart}'
      exit 1 ;;
```

## EXPLANATION

- 1 A script called functions is sourced to make functions defined there available to this script.
- 2 The RETVAL variable (which holds the function return value) is initialized to 0 and the prog variable is initialized to crond.
- 3 This line begins the definition for the start() function.
- 4 A message is displayed saying that the cron daemon is starting.
- 5 The daemon function is called with crond as its argument. (The function was defined in the functions script sourced at the beginning of the script.) The function attempts to start the crond daemon and returns a value of success (0) or failure (1).
- 6 The RETVAL variable is assigned the value of the status variable ?. It contains the value returned by the daemon() function. This value is used by the operating system to print an OK or FAILED message to the screen during the boot process.
- 7 The echo command prints a blank line to the screen.
- 8 If the return value indicates success (0 mean success) then a lock file for the cron daemon, /var/lock/subsys/crond, is created with the touch command.
- 9 The RETVAL variable is returned from the function.
- 10 This line begins the definition for the stop() function.
- 11 A message is displayed saying that the cron daemon is being stopped.
- 12 This calls the killproc() function, which is defined in the functions script sourced on line 1. It sends an argument of crond to this function. The function attempts to stop the daemon process and sends a return value based on its success or failure.
- 13 The RETVAL variable is assigned the value returned by the killproc() function, which is stored in $?.
- 14 A blank line is printed.
- 15 If the return value indicates success, the lock file for the cron daemon, /var/lock/subsys/crond, is deleted.
- 16 This defines the restart() function, which stops then starts the cron daemon.
- 17 The case command evaluates $1 and holds the value of the first argument sent to this script, either start or stop.
- 18 If the value of $1 is start, then the start() function is run.
- 19 If the value of $1 is stop, then the stop() function is run.
- 20 If the value of $1 is restart, then the restart() function is run.
- 21 Otherwise, a usage message is printed and the script will exit with status 1, failure.

## 16.4.3 Writing a Portable Script

System administrators often write shell scripts that work on multiple UNIX versions. Because commands change from UNIX to UNIX, your script will need to determine the UNIX version on which it is being run. This can be done using the uname command. Listed below are some popular versions of UNIX and the output of the uname command from each version. To create a script that will port to these different UNIX versions, your script should check the uname output and modify commands accordingly.

| UNIX Version: | uname Output: |
|---|---|
| AIX | AIX |
| FreeBSD | FreeBSD |
| HP-UX | HP-UX |
| IRIX | IRIX |
| Linux | Linux |
| Mac OS X | Darwin |
| NetBSD | NetBSD |
| OpenBSD | OpenBSD |
| SCO OpenServer 5 | SCO_SV |
| Solaris | SunOS |

A case command is commonly used to check for the operating system you are using. Example 16.15 checks for Linux (any brand), HP-UX, Solaris, FreeBSD, and Mac OS X UNIX.

### EXAMPLE 16.15

```
1  uname_out=`uname`
2  case "$uname_out" in
3  HP-UX) echo "You are running HP-UX"
4  SunOS) echo "You are running Solaris"
;;
FreeBSD) echo "You are running FreeBSD"
;;
Linux) echo "You are running Linux"
;;
Darwin) echo "You are running Mac OS X"
;;
*) echo "Sorry, $uname_out UNIX"
   echo "is not supported by this script"
;;
6  esac
```
