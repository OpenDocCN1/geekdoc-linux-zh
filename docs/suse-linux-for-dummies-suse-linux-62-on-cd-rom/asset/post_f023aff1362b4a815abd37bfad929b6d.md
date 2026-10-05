
# Appendix B: The linux man Pages 317

Don't be overwhelmed. If you deal with the options one at a time, you'll be able to understand how the command works. Take heart in the fact that most of the time, most people use one or two options.

If you issue the ls command, you will see that ls has many more options. That's why ls has been described as “a command that went bad intentions.”

# Description

The description section is a brief introduction to the command's functionality, which is then expanded on by what the options specify the command to do. A good example of a description is the manual page for man itself.

# Options

As stated in the “Synopsis” section, the options section tells how the command treats data in the arguments. Each option modifies the command's actions, drastically or subtly. The options can also pass information to the command about where to find files. The three types of options are:

- No argument
- Attached argument
- Positional argument

No argument means the option has a hyphen followed by one or more single-character options. For example:

```
[maddog@localhost maddog] > ps -ax
```

The a and x do not have any other values that they have to look at. However, in the following command:

```
[maddog@localhost maddog] > 1pq -Pzk1psa
```

the -P option to have an argument supplied; in this example, zk1psa.

# Environmental variables

Sometimes, to cut down on the information you have to give the command, you can set an environmental variable. Each shell (or command interpreter) has an environment that it works in. This environment (when it is created) consists of certain files that are open, some memory, and almost always some environmental variables.

Using the bash shell, type the following. (If you are not sure that you are using the bash shell, type bash at the command prompt and then continue with the example.)

```
[maddog@localhost maddog] > printenv
```

You see something like this:

```
USERNAME=
ENV=/home/maddog/.bashrc
HISTSIZE=1000
HOSTNAME=localhost.localdomain
LOGNAME=maddog
HFILESIZE=/var/spool/mail/maddog
TERMCAP=xterm|vs100|terminal emulator X11R6
WindowSystem:am:kn:mi:ms:xn:xo=co#80:it#24:n@d@:
AL=\E[d]:DC=\E[d]:PL=\E[dM]:DO=\E[dB]:IC=\:AL=\L:EL=as^N
AL=\E[d]:RI=\E[d]:UC=\E[u]:UP=\E[da]:ae=a:E[2j]:cm=\E[k]:dH=
B=1=g:cd=\E[J]:ce=\E[j]:ce=\E[\:ck=\E[1]:E=\E[11--kr=mE=
Cr=ms=\E[%i]:dr=ct=\E[3k]:dc=\E[pd]:dm=m^=
Jfe=\E[41]:ho=\E[H]:ic=\E[i]:tim=\E[4h]:is=\E[r]:rm=mE=
2J=\E[27]:hE=\E[27]:3:4:61=\E[41]:kr=\E[12]:-
k3=\E[13]:--k=\E[5]:ks=\E[15]:k66=\E[17]:k2=\E[18]:-
k4=\E[16]:k4=\E[12]:k5=\E[20]:k9=\E[21]:k=
^H=\E[EOB]:ke=\E[211]:kh=\E[k1]:E[OD]:kr=\E[EOC]:k
^H=\E[7H]:E=\E[1]:ku=\E[u0A:e=1^hm=\E[1m]:me=\E[m]:mr=\E[7m=
nd=\E[c]:rc=\E[8:sc=\E[7]:se=\E[m]:sf*j=so=\E[7m]:sr=
EM:ta=\E[t]:E[2j]:471?E8:ti=\E[7]:47h?ue=\E[m]:
u=up:us=\E[4m]
```

```
TERM=xterm
HOSTYPE=linux
PATH=/usr/local/bin:/usr/bin:/usr/X11R6:/usr/bin/mh:
/home/maddog
SHELL=/bin/bash
USER=maddog
HOSTDISPLAY=localhost.localdomain:0
  DISPLAY=:0
OSTYPE=Linux
WINDOWID=25165837
SHLVL=3
_/usr/bin/printenv
```

This list has lots of environmental variables, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

This list has lots of environmental variables, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

# Diagnostics

Error messages indicate that something has gone wrong. This is usually because of a bug.

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

Different shells, but we can't describe them all. Here are the most important ones:

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

# Bugs/Deficiencies

Some programs have bugs that are not documented in the manual page.

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

# Compatibility issues

When a new version of a command comes out, it may work slightly differently.

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

# Caveats

Caveats are warnings that the programmer wants to give the user about security issues or how much space the program uses.

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

# Disclaimers

Disclaimers are usually legal statements included at the insistence of the author's employer. They tell you that if you use this program and it harms someone.

- PATH tells all the places to look for commands
- HOME tells cd where to go when you don't supply any arguments
- OSTYPE tells the shell and what operating system they are on

# Authors

The authors are simply the people who wrote the command or program. Often, this section also explains how to report bugs or discuss new features you may want to see.

# Acknowledgments

The acknowledgments section, which is much more pleasant than the disclaimers section, recognizes the previous work put into a program that the author has built on. This is the essence of Linux and the GNU Public License, to allow and encourage people to build on others.

# Copyrights

People think Linux code or other freeware code is not copyrighted. This is typically not true. The authors of the code often take great care to copyright their code because they want credit for their work.
