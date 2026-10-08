# 312

# Hour 14

If you have vsh on your system, you might be interested in experimenting with this very different shell.

The zsh is another command shell, one written by Paul Falstad of Princeton University. The Bourne Again shell, bash, also appears in the listing, as does the mush program, which is an electronic mail package.

3. Needless to say, many shells are available! To change my login shell to any of these alternate shells, or even just to verify what I'm running, I can use the change shell command:

```
% chsh
Changing login shell for taylor.
Old shell: /bin/csh
New shell:
```

At this point, the program shows me I currently have /bin/csh as my login and asks me to specify an alternative shell. I'll try to confuse you by requesting emacs become my login shell:

```
% chsh
Changing shell for taylor.
Old shell: /bin/csh
New shell: /usr/local/bin/gnuacs
/usr/local/gnuacs is unacceptable as a new shell.
```

4. The program has some knowledge of valid shell names, and it requires you to specify one. Unfortunately, it doesn't divulge that information, so typing to ? to find what's available in the program complaining that ? is unacceptable as a new shell.

You can, peek into the file that etsh uses to confirm which programs are valid shells. I'll check /etc/shells and looks like this:

```
% cat /etc/shells
/bin/ksh
/bin/sh
/bin/csh
/usr/local/bin/csh
/usr/local/bin/tcsh
```

I'll change my shell from /bin/csh to /usr/local/bin/tcsh:

```
% chsh
Changing login shell for taylor
Old shell: /bin/csh
New shell: /usr/local/bin/tcsh
```

Notice that, in UNIX style, there is no actual confirmation that anything was done. I now conclude, that I did not get any error messages, the program worked. Fortunately, I can easily check by using etsh again or redoing the awk program with a C shell history command:

```
% ialah
awk -F: '{if ($1 == "taylor") print "your shell is: " $7}' < /etc/passwd
your shell is: /usr/local/bin/tcsh
```

![](bbox=[0.065, 0.893, 0.143, 0.963])