
Here is a shell program called mypgm1, which takes only one parameter (a name) and displays it on the screen:

```
#!/bin/sh
#Name display program
if [ $# -eq 0 ]
then
    echo "Name not provided"
else
    echo "Your name is "$1
fi
```

If you execute mypgm1, as follows,

$ bash mypgm1

you get the following output:

Name not provided

However, if you execute mypgm1, as follows,

$ bash mypgm1 Sanjiv

you get the following output:

Your name is Sanjiv

The shell program mypgm1 also illustrates another aspect of shell programming: the built-in variables provided to the shell by the Linux kernel. In mypgm1, the built-in variable $# provides the number of positional parameters passed to the shell program. You learn more about working with built-in variables in the next major section of this chapter.

## Using Positional Parameters to Access and Retrieve Variables from the Command Line

Using positional parameters in scripts can be helpful if you need to use command lines with piped commands requiring complex arguments. Shell programs containing positional parameters can be even more convenient if the commands are infrequently used. For example, if you use your Fedora system with an attached voice modem as an answering machine, you can write a script to issue a command that retrieves and plays the voice messages. The following lines convert a saved sound file (in .rmd or voice-phone format) and pipe the result to your system's audio device:

```
#!/bin/sh
# play voice message in /var/spool/voice/incoming
rm2topvf /var/spool/voice/incoming/$1 | pvfspeed -s 8000 ; \
pvftobasic >/dev/audio
```

A voice message can then easily be played back using this script (perhaps named pmm):

```
$ pmm name_of_message
```

Shell scripts that contain positional parameters are often used for automating routine and mundane jobs, such as system log report generation, file system checks, user resource accounting, printer use accounting, and other system, network, or security administration tasks.

### Using a Simple Script to Automate Tasks

You could use a simple script, for example, to examine your system log for certain keywords. If the script is run via your system's scheduling table, /etc/crontab, it can help automate security monitoring. By combining the output capabilities of existing Linux commands with the language facilities of the shell, you can quickly build a useful script to perform a task normally requiring a number of command lines. For example, you can create a short script, named greplog, like this:

```
#!/bin/sh
#	name:	greplog
#	use:	mail grep of designated log using keyword
#	version:	v.01 08aug02
#	author: bb

#	usage: greplog [keyword] [logpathname]

#	bugs: does not check for correct number of arguments

# build report name using keyword search and date
log_report=/tmp/$1.logreport.`date '+%m%dy'`

# build report header with system type, hostname, date and time
echo "====================================" \
		>$log_report
echo "				S Y S T E M	M O N I T O R	L O G" >>$log_report
echo uname -a >>$log_report
echo "Log report for" `hostname -f` "on" `date '+%c'` 		>>$log_report
echo "====================================" \
		>$log_report ; echo "" >>$log_report

# record log search start
echo "Search for->" $1 "starting" `date '+%r'` >>$log_report
echo "" >>$log_report

# get and save grep results of keyword ($1) from logfile ($2)
# build report footer with time
# mail report to root
# clean up and remove report
```

In this example, the script creates the variable $log_report, which will be the filename of the temporary report. The keyword ($1) and first argument on the command line is used as part of the filename, along with the current date (with perhaps a better approach to use $$ instead of the date, which will append the script's PID as a file extension). Next, the report header containing some formatted text, the output of the `uname` command, and the hostname and date is added to the report. The start of the search is then recorded, and any matches of the keyword in the log are added to the report. A footer containing the name of the report and the time is then added. The report is mailed to root with the search term as the subject of the message, and the temporary file is deleted.

> NOTE
> By default, Fedora uses the logwatch log monitoring command (actually a Perl script) in your system's `/etc/cron.daily` directory to generate various reports each day at 0402 (4:02 a.m.). Configure logwatch by editing the file `/etc/log.d/logwatch.conf`. Other system monitoring tools are included, such as `tripwire`. System logging can be controlled by editing `/etc/syslog.conf`.

You can test the script by running it manually and feeding it a keyword and a pathname to the system log, `/var/log/messages`, like this:

```
# greplog FAILED /var/log/messages
```

Note that your system should be running the `syslogd` daemon. If any login failures have occurred on your system, the root operator might get an email message that looks like this:

```
Date: Thu, 23 Oct 2003 16:23:24 -0400
From: root <root@stinkpad.home.org>
To: root@stinkpad.home.org
Subject: FAILED

==========================================================
SYSTEM MONITOR LOG
Linux stinky 2.4.22-1.2088.nptl #1 Thu Oct 9 20:21:24 EDT 2003 i686 i686 i386
+GNU/Linux
Log report for stinkpad.home.org on Thu 23 Oct 2003 04:23:24 PM EDT
==========================================================

Search for-> FAILED starting 04:23:24 PM

Oct 23 16:23:04 stinkpad login[1769]: FAILED LOGIN 3 FROM (null) FOR bball,
+Authentication failure

End of /tmp/FAILED.logreport.102303 at 04:23:24 PM
```

To further automate the process, you can include command lines using the script in another script to generate a series of searches and reports.

## Built-in Variables

Built-in variables are special variables provided to shell by Linux that can be used to make decisions within a shell program. You cannot modify the values of these variables within the shell program.

Some of these variables are:

- $# — Number of positional parameters passed to the shell program
- $? — Completion code of the last command or shell program executed within the shell program (returned value)
- $0 — The name of the shell program
- * — A single string of all arguments passed at the time of invocation of the shell program

To show these built-in variables in use, here is a sample program called mypgm2:

```
#!/bin/sh
#my test program
echo "Number of parameters is $#"
echo "Program name is $0"
echo "Parameters as a single string is $*"
```

If you execute mypgm2 from the command line in pdksh and bash as follows,

```
$ bash mypgm2 Sanjiv Guha
```

you get the following result:

Number of parameters is 2
Program name is mypgm2
Parameters as a single string is Sanjiv Guha

## Special Characters

Some characters have special meaning to Linux shells; these characters represent commands, denote specific use for surrounding text, or provide search parameters. Special characters provide a sort of shorthand by incorporating these rather complex meanings into a simple character. Some special characters are shown in Table 14.2.

**TABLE 14.2**
**Special Shell Characters**

| Character | Explanation |
| :--- | :--- |
| $ | Indicates the beginning of a shell variable name |
| ; | Pipes standard output to next command |
| # | Starts a comment |
| & | Executes a process in the background |
| ? | Matches one character |
| * | Matches one or more characters |
| > | Output redirection operator |
| < | Input redirection operator |
| ` | Command substitution (the backquote or backtick—the key above the Tab key on most keyboards) |
| >> | Output redirection operator (to append to a file) |
| << | Wait until following end-of-input string (HERE operator) |
| [ ] | Range of characters |
| [a-z] | All characters a through z |
| [a,z] or [az] | Characters a or z |
| Space | Delimiter between two words |

Special characters are very useful to you when you’re creating shell scripts, but if you inadvertently use a special character as part of variable names or strings, your program will behave incorrectly. As you learn in later parts of this section, you can use one of the special characters in a string if you precede it with an *escape character* (\ , or backslash) to indicate that it isn’t being used as a special character and shouldn’t be treated as such by the program.

A few special characters deserve special note. They are the double quotes (") , the single quotes ('), the backslash (\), and the backtick (`)—all discussed in the following sections.
