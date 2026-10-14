If you don’t specify a section, man will search sections that cover commands first; typically, the order will be sections 1, 8, and 6.

It is possible that a command is described in more than one section of the manual. To view a document specific section, specify the man command like this:

```
man section command
```

In the preceding example, the man command is listed twice: in sections 1 and 7. To read the information on section 7, enter this command:

```
man 7 man
```

# Getting a Brief Command Description: whatis

Sometimes you don’t care to read five paragraphs of the UNIX manual just to find out what a command does. In those cases, the whatis tool can also be used to obtain a brief description of the command. To operate in this mode, you provide the name of the tool as an argument.

Check This Out: Building the whatis Database: makewhatis
To build the whatis database, you’ll need to use the makewhatis command. To start building the database, enter this command:

```
/usr/sbin/makewhatis
```

Note that you must be root (you can also be su and execute the command) in order for this program to work properly. After a few moments, the database will be built. If you have an older computer, this action could take a while.

whatis will print out a one-line description of what a command does. I have found that whatis is a great exploration tool. If you go into a program directory such as /sbin, you can quickly learn what the commands there do by issuing this command:

```
cd directory; whatis *
```

This will take you to the directory you specify under directory and issue a whatis on all the files that it finds there. The * is a regular expression that specifies all files it finds in that directory:

```
[alberto@localhost alberto]$ cd /sbin; whatis *
adjtimex (2)          - tune kernel clock
adjtimex (8)          - display or set the kernel time variables
arp (8)               - manipulate the system ARP cache
(And more...)
```

# Searching Standard Locations: whereis

Sometimes the help you need is in locating the file or program you’re looking for. As explained earlier, your shell finds commands by looking into your environment variable. When you issue the name of a command, the directories listed in the PATH environment variable are searched for a matching command. If found, the command is executed; otherwise, you get the dreaded “command not found” response.

Because some directories holding tools are not included in the default user path, your shell will not see them. In those cases, you can use the whereis tool to find the actual path to the tool you want to use.

Note:
For more information on regular expressions, take a look at Chapter 14, “Putting the Shell to Work.”

Not only does whereis locate a binary, but it will also locate source and manual pages having the name you