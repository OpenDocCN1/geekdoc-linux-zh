```
```
This is the end of test script.
$ 
$ ps
  PID TTY          TIME CMD
 1637 pts/0    00:00:00 bash
 1718 pts/0    00:00:00 ps
$ 
```

```

It worked perfectly. All three designated signals were ignored, and the script ran in the background without interruption. Here’s the controlling script in its entirety for your perusal:

```
```
$ cat trapandrunc.sh
#!/bin/bash
# Set specified signal traps; then run script in background
#
############### Check Signals to Trap
###############
#
while getoptps S: opt   #Signals to trap listed with -S option
do
	case "$opt" in
	S)
		# Found the -S option
		signalList="" #Set signalList to null
		#
		for arg in $OPTARG
		do
			case $arg in
			1)
				#SIGHUP signal is handled
				signalList=$signalList"SIGHUP "
			;;
			2)
				#SIGINT signal is handled
				signalList=$signalList"SIGINT "
			;;
			20)
				#SIGTSTP signal is handled
				signalList=$signalList"SIGTSTP "
			;;
			*)
				#Unknown or unhandled signal
				echo "Only signals 1 2 and/or 20 are
				allowed."
				echo "Exiting script..."
				exit
			;;
		esac
	done
	;;
	*)
		echo 'Usage: -S "Signal(s)" script-to-run-name'
```

```