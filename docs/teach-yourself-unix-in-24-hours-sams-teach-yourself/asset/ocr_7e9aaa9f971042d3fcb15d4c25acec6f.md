4 USER=taylor
5 PATH=:/users/taylor/bin:/bin:/usr/bin:/ucb:/usr/local:/etc:
/usr/etc:/usr/local:/usr/unsup/bin:
6 MAIL=/usr/spool/mail/taylor
7 LOGNAME=taylor
8 EDITOR=ucb/bin/vi
9 NAME=Dave Taylor
10 EXIT=set Ignorecase
11 RNINT=-message -reference -hdate -hsender -hsummary -hreply
-hdistr -hlines -hollow -hnkeys -hkey -hreturn -hto
-ho-original -sun-xo -htx -horiginator -hntnp
12 SUBLINE=_ % Educational computing, School of Education

This probably seems quite overwhelming. What are all these things, and why on earth should they matter? Matter because it is important for you to learn exactly how your environment is set up so that you can change things if you desire. As soon as will be to recognize, I have modified much of my system's environment so that the C shell does what I want it to, rather than what its default would tell it to.

When I log in to the system, the system defines some environment variables, indicating where my home directory is located, what I'm running, and so on. These variables are listed in Table 14.1.

# Table 14.1. Default variables set by UNIX upon login.

| Variable | Description |
| --- | --- |
| HOME | This is my home directory, obtained from the fourth field of the password file. Try the command
`grep $HOME /etc/passwd | awk -F: ' '{print $6}'`
to see what your home directory is set, or just use env HOME or echo $HOME. This is not the directory that I start in, but it's also the directory that cd moves back to when I don't specify a different directory. My HOME variable is as /users/taylor. |
| SHELL | When UNIX programs, as vi, process the t command to execute UNIX commands, they check this to see which shell I'm using. If I were to type : followed by Return in vi, the program would create a new C shell for me. If I had SHELL=/bin/vi, I would start a Bourne shell. My SHELL variable is set to /bin/csh |
| TERM | By default, your terminal is defined by the value of this environment variable, which starts out as unknown. (When you first run it, the program would complain unknown: terminal not known.) Many sites know what kind of terminals are using lines, however so this variable is set to the correct value you even see it. If it's not set, you can define it to the appropriate value within your .login file. (You will learn to do this later in the hour.) |

![](bbox=[0.095, 0.893, 0.155, 0.963])