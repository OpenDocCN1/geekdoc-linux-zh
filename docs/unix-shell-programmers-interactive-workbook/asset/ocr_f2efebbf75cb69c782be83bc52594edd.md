# LAB I.I EXERCISES

I.I.I SET UP FOR LINUX AND OTHER UNIX SYSTEMS

The KornShell is an executable program named ksh. You can download an executable copy for most UNIX systems, including LINUX, using the following URL:

```
http://research.att.com/sw/tools/reuse
```

In the middle of this web page is a button marked Binary under a heading that says "Non-Commercial License Agreement and Available Software." Click the button, and you will go to a page that lists several software packages and gives you a menu of operating systems for each one. Select "ast-base-97" or "ast-base-98" (whichever lists your operating system), accept the license agreement, and proceed to download and install the software as instructed.

An alternative way to get the very latest release of the KornShell for AIX, HPUX, IRIX, Solaris, SunOS, or UnixWare is through Global Technologies Ltd., which you can contact using the following URL:

```
http://www.gtlincinc.com
```

Once ksh is installed on your system, you have a choice of running it as your default shell or using some other shell as your default and running ksh as a command.

The way to make your default shell is to use an interactive program named chsh (change shell) on some systems or passwd with a particular set of options on other systems. For example, I have a local account on a DEC OSF/I system and use the chsh command to do this. I also have a networked account on a Solaris system, and the command I use is passwd -r nisplus -e. In either event, the command shows me the pathname of my current shell, and asks me for the pathname of the shell that I want to be my new default. Once you change your default shell every time you log into your system, the KornShell will start running and will interpret the command lines that you type. If you are not sure about this, you might want to run the