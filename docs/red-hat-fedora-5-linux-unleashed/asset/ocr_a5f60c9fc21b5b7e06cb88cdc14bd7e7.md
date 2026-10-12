you get the following output

```
Name not provided
```

However, if you execute mypm, as follows,

```
```
& bash  mypm Sanjiv
```
```

you get the following output:

```
Your name is Sanjiv
```

The shell program mypm also illustrates another aspect of shell programming: the built-in variables provided to the shell by the Linux kernel. In mypm, the built-in variable $# provides the number of positional parameters passed to the shell program. You learn more about working with built-in variables in the next major section of this chapter.

# ### Using Positional Parameters to Access and Retrieve Variables from the Command Line

Using positional parameters in scripts can be helpful if you need to use command lines with piped commands requiring complex arguments. Shell programs containing positional parameters can be even more convenient if the commands are infrequently used. For example, if you use your Fedora system with an attached voice modem as an answering machine, you can write a script to issue a command that retrieves and plays the voice messages. The following lines convert a saved sound file (in .rm or voice-phone format) and pipe the result to your system's audio device:

```
```
#!/bin/sh
# play voice message in /var/spool/voice/incoming
rmtoopvf /var/spool/voice/incoming/$1 | pvfspeed -s 8000 | \
pvftobasic >/dev/audio
```
```

A voice message can then easily be played back using this script (perhaps named pmm):

```
```
$ pmm name_of_message
```
```

Shell scripts that contain positional parameters are often used for automating routine and mundane jobs, such as system log report generation, file system checks, user resource accounting, printer use accounting, and other system, network, or security administration tasks.

# ### Using a Simple Script to Automate Tasks

You could use a simple script, for example, to examine your system log for certain keywords. If the script is run via your system's scheduling table, /etc/crontab, it can help automate security monitoring. By combining the output capabilities of existing Linux commands with the language facilities of the shell, you can quickly build a useful script