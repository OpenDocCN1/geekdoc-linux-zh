In 1978, Stephen Bourne replaced the original UNIX shell with a new one that added advanced scripting capabilities and command-line editing. The Bourne shell, as it is called, is still available; you can try it from your Linux machine by entering /bin/sh from a terminal screen.

Bill Joy (more recently known as one of the Scientists who created Java), while he was at the University of Berkeley at Southern California, created the C shell. The C shell has more job-control features than the Bourne shell and sports c-like syntax. And, the C shell is available on Linux. You can try it by typing /bin/c. This "shell" goes on: there is a shell Korn; OS/400 has one called Q; and there are many others. Eventually, a group of UNIX programmers combined the features of several shells into one called bash (a play on words that stands for the "Bourne Again Shell"). The bash shell, because of its powerful features, was selected as the default Linux shell.

If you become attached to a shell other than bash, you can change to it by modifying your user profile in the /etc/passwd file. Each entry in the passwd file contains a semicolon-separated list of options:

```
username:password:userid:groupid:user_description:home_dir
```

The following line qualifies the shell as /bin/bash in one of the authors' passwd file entries:

```
donat:x:500:500::/home/donat:/bin/bash
```

To give an idea of the powerful yet quirky features of bash, rather than using an editor or the less command to view the /etc/passwd file, you can use the following command to list your default shell (replacing username with your user name):

```
$ cat /etc/passwd | grep Username | cut -d -f 7
```

It reports by listing /bin/bash to your terminal screen.

> Note: The dollar symbol is the bash prompt when you are logged on as a normal user. When you are logged in as root, the shell prompt will have a pound symbol (#). Commands that require root privileges are identified in this chapter with the # symbol; otherwise, the $ symbol is displayed.

Another way to list your default shell is by echoing the SHELL environment variable:

```
$ echo SHELL
```

Once again, it simply lists /bin/bash to your terminal screen.

These echo and cat commands use some of the powerful features of the bash shell: piping and environment variables. In this chapter, you'll learn not only about environment variables and piping, but also features like file redirection, filename globbing, and substitution mechanisms—in other words, how to become a power shell user.