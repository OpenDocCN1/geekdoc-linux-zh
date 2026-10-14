# Good Locations For Scripts

The ~/bin directory is a good place to put scripts intended for personal use. If we write a script that everyone on a system is allowed to use, the traditional location is /usr/local/bin. Scripts intended for use by the system administrator are often located in /usr/local/sbin. In most cases, locally supplied software, whether scripts or compiled programs, should be placed in the /usr/local hierarchy and not in /bin or /usr/bin. These directories are specified by the Linux Filesystem Hierarchy Standard to contain only files supplied and maintained by the Linux distributor.

# More Formatting Tricks

One of the key goals of serious script writing is ease of maintenance; that is, the ease with which a script may be modified by its author or others to adapt it to changing needs. Making a script easy to read and understand is one way to facilitate easy maintenance.

# Long Option Names

Many of the commands we have studied feature both short and long option names. For instance, the ls command has many options that can be expressed in either short or long form. For example:

```
[me@linuxbox ~]$ ls -ad
```

and:

```
[me@linuxbox ~]$ ls --all --directory
```

are equivalent commands. In the interests of reduced typing, short options are preferred when entering options on the command line, but when writing scripts, long options can provide improved readability.

# Indentation And Line Continuation

When employing long commands, readability can be enhanced by spreading the command over several lines. In Chapter 18, we looked at a particularly long example of the find command: