Another special syntax overrides the value of a *make* variable. For example, GNU *make* uses the `CFLAGS` variable to hold the flags used when compiling C files. You can override the value of this variable when you invoke *make*. Here is an example of how you can define `CFLAGS` as the option `-g -O2`:

```
make CFLAGS="-g -O2"
```

In addition to these options, GNU *make* accepts several other command-line options. Table 1-3 lists the GNU *make* options.

**Table 1-3 Options for GNU make**
| Option | Meaning |
|:-|:-|
| -b | Ignore but accept for compatibility with other versions of make |
| -C DIR | Change to the specified directory before reading the makefile |
| -d | Print debugging information |
| -e | Allow environment variables to override definitions of similarly named variables in the makefile |
| -f FILE | Read FILE as the makefile |
| -h | Display the list of make options |
| -i | Ignore all errors in commands executed when building a target |
| -I DIR | Search specified directory for included makefiles. (The capability to include a file in a makefile is unique to GNU make.) |
| -j NUM | Specify the number of commands that make can run simultaneously |
| -k | Continue to build unrelated targets, even if an error occurs when building one of the targets |
| -l LOAD | Don't start a new job if load average is at least LOAD (a floating-point number) |
| -m | Ignore but accept for compatibility with other versions of make |
| -n | Print the commands to execute, but do not execute them |
| -o FILE | Do not rebuild the file named FILE, even if it is older than its dependents |
| -p | Display the make database of variables and implicit rules |
| -q | Do not run anything, but return 0 (zero) if all targets are up to date; return 1 if anything needs updating; and 2 if an error occurs |
| -r | Get rid of all built-in rules |
| -R | Get rid of all built-in variables and rules |
| -s | Work silently (without displaying the commands as they execute) |
| -t | Change the timestamp of the files |