# EXPLANATION (CONTINUED)

+   4 The bang (!) with the dollar sign ($) refers to the last argument of the last command on the history list. The last argument is c.
+   5 The caret (^) represents the first argument after the command. The bang (!) with the ^ refers to the first argument of the last command on the history list. The first argument of the last command is a.
+   6 The asterisk (*) represents all arguments after the command. The bang (!) with the * refers to all of the arguments of the last command on the history list.
+   7 The last command from the history list is printed but not executed. The history list is updated. You could now perform caret substitutions on that line.

# 9.4 Aliases

An alias is a C/TC shell user-defined abbreviation for a command. (For tcsh enhancements to the alias mechanism, see "TC Shell Aliases" on page 491.) Aliases are useful when a command has a number of options and arguments or the syntax is difficult to remember. Aliases set at the command line are not inherited by subshells. Aliases are normally set in the .cshrc or .tcshrc file. Because the .cshrc or .tcshrc is executed when a new shell is started, any aliases set there will get reset for the new shell. Aliases may also be passed into shell scripts, but will cause potential portability problems unless they are directly set within the script.

# 9.4.1 Listing Aliases

The alias built-in command lists all set aliases. The alias is printed first, followed by the real command or commands it represents.

# EXAMPLE 9.20

```
% alias
co      compress
cp      cp -i
ls1     enscript -B -r -Porange -f Courier8 !* &
mailq   /usr/lib/sendmail -bp
mroe    more
mv      mv -i
rn      /usr/spool/news/bin/rn3
uc      uncompress
uu      uudecode
vg      vgrind -t -s11 !:1 | lpr -t
weekly  (cd /home/jody/ellie/activity; ./weekly_report; echo Done)
```

# EXPLANATION

The alias command lists the alias (nickname) for the command in the first column and the real command or commands the alias represents in the second column.