```
case is a keyword
ulimit is a shell builtin
history is an exported alias for fc -l
```

If a single command is searched, type's exit code can be used to determine if that command can be found in the search path $PATH. If a command can be found, type exits with an exit code of 0 indicating success or 1 indicating failure. For example, the following function allows you to determine whether particular commands exist on the system:

```
haveCMD () {
  type "$1" > /dev/null 2>&1
  return $?
}
```

# The sleep Command

The sleep command pauses for a given number of seconds. The basic syntax is

```
sleep n
```

where n is the number of seconds to sleep or pause. Some types of UNIX enable other time units to be specified. It is usually recommended that n not exceed 65,534.

The sleep command can be used to give a user time to read an output message before clearing the screen. It can also be used when you want to give a series of beeps:

```
echo -e "A value must be input!\a"
sleep 1
echo -ne "\a"
sleep 1
echo -ne "\a"
```

\a causes echo to output an audible beep. The -e option is required on some UNIX systems for \a to sound a beep. The -n option suppresses the newline that echo normally prints. The sleep command is used in the previous example to give a sequence of beeps, spaced one second apart.

sleep can be used in a loop to repeat a job periodically:

```
while :
do
  date
  who
  sleep 300
done >> logfile
```

This code enables a list of users logged into the system to be appended to logfile every five minutes (300 seconds). If you want to leave this code running all the time, you must clear logfile periodically so that it does not eat up all your disk space.