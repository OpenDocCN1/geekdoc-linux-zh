# METHOD #2

You can also use GNU uname to output the CPU processor type of the system (such as i686, PowerPC, etc.); specify this with the -m option.

⇒ To output the CPU processor type of the system, type:

```
# uname -m [RET]
```

# A.7.3 Displaying Memory Usage

Use free to display system memory usage. It displays both physical memory and swap memory, giving values for total memory available on the system, amount used, and amount free. The output is displayed in kilobytes; use -b to display in bytes, and -m to display in megabytes. The -t switch will also display a list of totals for all of the types of memory on the system.

⇒ To output a report on current system memory usage, in megabytes, and with a line of calculated total values, type:

```
# free -m -t [RET]
```

# A.7.4 Displaying the Linux Version

Use the GNU uname tool to see what version of Linux you are running. By default, it outputs the name of the operating system.

⇒ To output the name of the operating system, type:

```
# uname [RET]
```

Use the -r option to output the operating system release number.

⇒ To output the release number of the operating system, type:

```
# uname -r [RET]
```

The -a option is useful; it outputs all information about the system that it can, including OS name and release number, CPU type, plus the version date and number of the operating system and the machine's hostname.

⇒ To output all of the uname information for the system you are on, type:

```
# uname -a [RET]
```

# A.7.5 Displaying the Distribution Version

The version of the installed distribution is kept in a particular file in /etc, whose name depends on the distribution. These are listed in the following table. Use cat to display the contents of this file.