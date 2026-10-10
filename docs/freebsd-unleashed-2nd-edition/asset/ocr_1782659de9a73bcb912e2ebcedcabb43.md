Now *that* looks more useful—especially the **grep** series of commands. These seem to be tools for searching for patterns within files, as you hoped. You could now type **man grep** to read the man page for *grep*, and you would find that indeed this command does what you need.

# ## Command Summaries

At other times, you might know the name of a command but are not sure what it does (if you are poking around in /usr/bin or /usr/games, for example). You can use the -f option to man to get a short, one-line description of a command. For example, suppose you find the command pom in the /usr/games directory, and you want to know what it does:

```
```
# man -f pom
pom(6) - display the phase of the moon
bash$
```
```

The (6) at the end of the command name is the section of the manual that the command comes from.

# ## Manual Sections

The online manuals are divided into nine sections, as detailed in Table 7.1.

TABLE 7.1 | Manual Sections
| Section | Description |
| :--- | :--- |
| 1: User Commands | Information on user commands such as 1s, rm, cp, and grep. This is the section you will probably use most often while working with and learning FreeBSD. |
| 2: System Calls | Contains information on various APIs for FreeBSD. This section is primarily of interest to C programmers. |
| 3: Subroutines | This section contains information on subroutines, also known as library functions. Once again, mostly of interest to C programmers. |
| 4: Devices | More stuff for C programmers. Contains information on interfacing with device drivers in FreeBSD. |
| 5: File Formats | Contains information on the formats of various system configuration files, such as the crontab files for the scheduling of regular jobs and the rc files for controlling system startup. |
| 6: Games | The most important section of the manual. This section contains instructions for playing the various games and other amusements that come with FreeBSD. |
| 7: Miscellaneous | If your topic doesn't fit anywhere else, it will be found here. |
| 8: System Administration | Contains information on commands related to system administration, such as fsck, for checking filesystems. |
| 9: Kernel Interfaces | More information for programmers. This section contains information on interfacing with the kernel in C. |