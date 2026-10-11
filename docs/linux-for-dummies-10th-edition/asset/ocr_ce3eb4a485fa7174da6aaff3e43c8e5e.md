![](bbox=[0.16, 0.09, 0.25, 0.19])

If you experiment heavily with these files, create a separate user account so that you can do whatever you want without messing up your own login. This advice especially goes for /etc/profile. You can damage everyone’s login with this one! To create a separate /etc/profile, you can make a backup by typing cp /etc/profile /etc/profile. original. Then edit /etc/profile knowing that you can always delete it with the rm command and use the mv command to rename /etc/profile. original to /etc/profile.

To create an environment variable from scratch, you typically name it with all capital letters and then you "export" it. For example:

```
CUSTOMVAR="new variable"
export CUSTOMVAR
```

Don't be too discouraged if you don't understand all this variable stuff right now. As you become more proficient with Linux, you should explore shell scripting. Shell scripting is the art of creating computer programs with just the shell. Most Linux and UNIX Administrators speak shell script language like you and I speak our native tongues.

# # Using Redirection and Pipes

Redirection and pipes facilitate the flow of information. A pipe is exactly what it sounds like: It directs the output of one program to the input of another program. A pipeline may consist of several utilities plumb ed together by pipes. At either end of this pipeline is, optionally, a redirection.

Almost all Linux utilities that require input and output have been plumbed with the following common interfaces: stdin (standard input — typically the keyboard), stdout (standard output — typically the monitor), and stderr (standard error — typically also the monitor). By having a common method to feed input to a program or read data from the output of a program, you can glue utilities together into sophisticated solutions.

# ## Redirecting command output

I discuss redirecting command output here because it's by far the most common form of information detouring. One example of output redirection involves telling a command to send its results to a file rather than to the screen, as you probably have been used to seeing. Start in some familiar territory by typing ls -la ~ and then pressing Enter, to produce something like the following: