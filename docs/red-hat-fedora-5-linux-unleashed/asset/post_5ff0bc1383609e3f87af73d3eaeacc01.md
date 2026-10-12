
## Using Variables in Shell Scripts

When writing shell scripts for Linux, you work with three types of variables:

- **Environment variables**—Part of the system environment, you can use them in your shell program. New variables can be defined, and some of them, such as **PATH**, can also be modified within a shell program.
- **Built-in variables**—These variables, such as options used on the command (interpreted by the shell as a *positional argument*), are provided by Linux. Unlike environment variables, you cannot modify them.
- **User variables**—Defined by you when you write a shell script. You can use and modify them at will within the shell program.

A major difference between shell programming and other programming languages is that in shell programming, variables are not *typed*—that is, you do not have to specify whether a variable is a number or a string, and so on.

## Assigning a Value to a Variable

Assume that you want to use a variable called **1count** to count the number of iterations in a loop within a shell program. You can declare and initialize this variable as follows:

| Command | Environment |
| :--- | :--- |
| 1count=0 | pdksh and bash |
| set 1count=0 | tcsh |

> **NOTE**
> Under pdksh and bash, you must ensure that the equal sign (=) does not have spaces before and after it.

To store a string in a variable, you can use the following:

| Command | Environment |
| :--- | :--- |
| myname=Sanjiv | pdksh and bash |
| set myname=Sanjiv | tcsh |

Use the preceding variable form if the string doesn't have embedded spaces. If a string has embedded spaces, you can do the assignment as follows:

| Command | Environment |
| :--- | :--- |
| myname="Sanjiv Guha" | pdksh and bash |
| set myname="Sanjiv Guha" | tcsh |

## Accessing Variable Values

You can access the value of a variable by prefixing the variable name with a $ (dollar sign). That is, if the variable name is *var*, you can access the variable by using **$var**.

If you want to assign the value of *var* to the variable **1count**, you can do so as follows:

| Command | Environment |
| :--- | :--- |
| 1count=$var | pdksh and bash |
| set 1count=$var | tcsh |

## Positional Parameters

It is possible to pass options from the command line or from another shell script to your shell program.

These options are supplied to the shell program by Linux as *positional parameters*, which have special names provided by the system. The first parameter is stored in a variable called **1** (number 1) and can be accessed by using **$1** within the program. The second parameter is stored in a variable called **2** and can be accessed by using **$2** within the program, and so on. One or more of the higher numbered positional parameters can be omitted while you’re invoking a shell program.

Understanding how to use these positional parameters and how to access and use variables retrieved from the command line is necessary when developing more advanced shell programs.

## A Simple Example of a Positional Parameter

For example, if a shell program **mypgm** expects two parameters—such as a first name and a last name—you can invoke the shell program with only one parameter, the first name. However, you cannot invoke it with only the second parameter, the last name.

Here is a shell program called **mypgm1**, which takes only one parameter (a name) and displays it on the screen:

```bash
#!/bin/sh
#Name display program
if [ $# -eq 0 ]
then
    echo "Name not provided"
else
    echo "Your name is $1"
fi
```

If you execute **mypgm1**, as follows,

```bash
$ bash mypgm1
```

you get the following output

```text
Name not provided
```

However, if you execute mypm, as follows,

```bash
& bash mypm Sanjiv
```

you get the following output:

```text
Your name is Sanjiv
```

The shell program mypm also illustrates another aspect of shell programming: the built-in variables provided to the shell by the Linux kernel. In mypm, the built-in variable $# provides the number of positional parameters passed to the shell program. You learn more about working with built-in variables in the next major section of this chapter.

### Using Positional Parameters to Access and Retrieve Variables from the Command Line

Using positional parameters in scripts can be helpful if you need to use command lines with piped commands requiring complex arguments. Shell programs containing positional parameters can be even more convenient if the commands are infrequently used. For example, if you use your Fedora system with an attached voice modem as an answering machine, you can write a script to issue a command that retrieves and plays the voice messages. The following lines convert a saved sound file (in .rm or voice-phone format) and pipe the result to your system's audio device:

```bash
#!/bin/sh
# play voice message in /var/spool/voice/incoming
rmtoopvf /var/spool/voice/incoming/$1 | pvfspeed -s 8000 | \
pvftobasic >/dev/audio
```

A voice message can then easily be played back using this script (perhaps named pmm):

```bash
$ pmm name_of_message
```

Shell scripts that contain positional parameters are often used for automating routine and mundane jobs, such as system log report generation, file system checks, user resource accounting, printer use accounting, and other system, network, or security administration tasks.

### Using a Simple Script to Automate Tasks

You could use a simple script, for example, to examine your system log for certain keywords. If the script is run via your system's scheduling table, /etc/crontab, it can help automate security monitoring. By combining the output capabilities of existing Linux commands with the language facilities of the shell, you can quickly build a useful script to perform a task normally requiring a number of command lines. For example, you can create a short script, named `greplog`, like this:

```shell
#!/bin/sh
#  name:  greplog
#  use: mail grep of designated log using keyword
#  version:  v.01 0@Aug02
#
#  author: bb
#
#  usage: greplog [keyword] [logfilepathname]
#
#  bugs: does not check for correct number of arguments

# build report name using keyword search and date
log_report=/tmp/$1.logreport.`date '+%m%d%y'`

# build report header with system type, hostname, date and time
echo "==================================================" \
      >$log_report
echo "        SYSTEM MONITOR LOG" >>$log_report
echo uname -a >>$log_report
echo "Log report for" `hostname -f` `on ` `date '+%c'`   >>$log_report
echo "==================================================" \
      >$log_report ; echo "" >>$log_report

# record log search start
echo "Search for->" $1 "starting" `date '+%r'` >>$log_report
echo "" >>$log_report

# Get and save grep results of keyword ($1) from logfile ($2)
grep -i $1 $2 >>$log_report

# build report footer with time
echo "" >>$log_report
echo "End of" $log_report `at ` `date '+%r'` >>$log_report

# mail report to root
mail -s "Log Analysis for $1" root <$log_report

# clean up and remove report
rm $log_report
exit 0
```

In this example, the script creates the variable `$log_report`, which will be the filename of the temporary report. The keyword ($1) and first argument on the command line is used as part of the filename, along with the current date (with perhaps a better approach to use $$ instead of the date, which appends the script’s PID as a file extension). Next, the report header containing some formatted text, the output of the uname command, and the hostname and date is added to the report. The start of the search is then recorded, and any matches of the keyword in the log are added to the report. A footer containing the name of the report and the time is then added. The report is mailed to root with the search term as the subject of the message, and the temporary file is deleted.

> **NOTE**
> By default, Fedora uses the logwatch log monitoring command (actually a Perl script) in your system’s /usr/sbin/daily directory to generate various reports each day at 04:02 (4:02 a.m.). Configure logwatch by editing the file /etc/log.d/logwatch.conf. Other system monitoring tools are included, such as tripwire. System logging can be controlled by editing /etc/syslog.conf.

You can test the script by running it manually and feeding it a keyword and a pathname to the system log, /var/log/messages, like this:

```bash
# greplog FAILED /var/log/messages
```

Note that your system should be running the syslogd daemon. If any login failures have occurred on your system, the root operator might get an email message that looks like this:

```text
Date: Thu, 23 Oct 2003 16:23:24 -0400
From: root <root@stinkpad.home.org>
To: root@stinkpad.home.org
Subject: FAILED

================================================================
               S Y S T E M  M O N I T O R  L O G
================================================================
Linux stinky 2.4.22-1.2088.nptl #1 Thu Oct 9 20:21:24 EDT 2003 i686 i686 i386
+GNU/Linux
Log report for stinkpad.home.org on Thu 23 Oct 2003 04:23:24 PM EDT
================================================================

Search for -> FAILED starting 04:23:24 PM

Oct 23 16:23:04 stinkpad login[1769]: FAILED LOGIN 3 FROM (null) FOR bball, +Authentication failure

End of /tmp/FAILED.logreport.102303 at 04:23:24 PM
```

To further automate the process, you can include command lines using the script in another script to generate a series of searches and reports.
