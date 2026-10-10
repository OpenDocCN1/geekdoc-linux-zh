Notice that this code section uses while and for loops (Chapter 13, “More Structured Commands”), as well as a case statement (Chapter 12, “Using Structured Commands”) to process through the -s option and its accompanying signal numbers. The only signals allowed for trapping with this script are SIGUP (1), SIGINT (2), and SIGSTP (20). If an option besides -s is used or incorrect signals to trap are listed, “error” messages are provided to the script user.

After the -s option and its parameters are processed, the script determines if a script name was provided using $@ stored in the $OPTIND environment variable:

```
shift $[ $OPTIND - 1 ] #Script name should be in parameter #
if [ -z $@ ]
then	echo
	echo 'Error: Script name not provided.'
	echo 'Usage: -S "Signal(s)" script-to-run-name'
	echo 'Exiting script...'
	exit
elif [ -o $@ ] && [ -x $@ ]
then	scriptToRun=$@
	scriptOutput="$@.out"
else	echo
	echo "Error: $@ is either not owned by you or not executable."
	echo "Exiting..."
	exit
fi
```

If the script name parameter is provided, a few additional checks are done to ensure that the script file is owned by the script user and that it is executable via if - then and elif statements (Chapter 12). If all is well, the script’s name is stored in another variable, scriptToRun , which is not essential but adds to the code’s clarity. Additionally, an output file is created that contains the script’s name and tacks on .out. Now that we have the script’s name we need to run and the signals to block, we’re ready to trap signals and kick off the script: