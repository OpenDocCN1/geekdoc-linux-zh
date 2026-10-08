# ACTION

+   1. To begin, use cat to list the contents of my .login file. Remember that any line
beginning with a # is a comment and is ignored.

```
% cat .login
#
# @($)Revision: 62.2 $\$
setenv TERM vt100
stty "^H" "^U" intr "^C" eof "^D"
stty crtybs crterase      # special DYNIX stuff for bs processing
# shell vars
set noclobber history=100 savehist=50 filec
# set up some global environment variables...
setenv ignorecase
# Some RN related variables...
setenv RNINIT      -hmessage -reference -hdate-r -hsender -summary
hthely -dhistr -htlines -hline -hfoillow -hnews -hkey -hresent -htreturn
hto -ht-original -hx-sun -hx-nodeoriginator -hnntp
setenv SUBLINE       "-st--%s"
setenv ORGANIZATION  "Educational Computing group, School of Education
```

setenv NAME "Dave Taylor"

newmail

mesg y
This is pretty straightforward, once you remove all the comments. Three different
kinds of environmental configuration commands are: setenv, stty, and set.
The setenv command defines environment variables; indeed, you can see that
m of the variables shown in the previous unit are defined in my .login file.
I use stty to set specific configuration options related to my
terminal (stty "set tty driver options\ I use this to ensure that ^h
erase (Backspace), ^u is a convenient shortcut allowing me to kill an entire line, and
^c sends an interrupt to a running program. I indicate the end of a file (EOF) with
^d. The second line of the preceding output example indicates that the CRT is
capable of backspacing and erasing characters on the display.

![](bbox=[0.065, 0.876, 0.138, 0.959])