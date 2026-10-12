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

# ## Using Positional Parameters to Access and Retrieve Variables from the Command Line

Using positional parameters in scripts can be helpful if you need to use command lines with piped commands requiring complex arguments. Shell programs containing positional parameters can be even more convenient if the commands are infrequently used. For example, if you use your Fedora system with an attached voice modem as an answering machine, you can write a script to issue a command that retrieves and plays the voice messages. The following lines convert a saved sound file (in .rmd or voice-phone format) and pipe the result to your system's audio device:

```
#!/bin/sh
# play voice message in /var/spool/voice/incoming
rm2topvf /var/spool/voice/incoming/$1 | pvfspeed -s 8000 ; \
pvftobasic >/dev/audio
```