and expects a carriage return to be implied. If your printer is expecting DOS-style carriage return and linefeed combinations but is only receiving a linefeed, it will advance the paper but never return the print head to the beginning of the line. There are a few ways you might be able to solve this problem.

The first is to look for an option in your printer's configuration that changes the way it interprets a linefeed character. See your printer documentation to see whether there is a way you can do this.

The second way is to create a filter that converts the LF to a combination of CR and LF. If your printer understands HP-PCL language, the following filter is recommended by the *FreeBSD Handbook* for performing this task:

```
```
#!/bin/sh
#
# hpif - Simple text input filter for lpd for HP-PCL based printers
# Installed in /usr/local/libexec/hpif
#
# Simply copies stdin to stdout.  Ignores all filter arguments.
# Tells printer to treat LF as CR+LF.  Ejects the page when done.

printf "\033&k2G" && cat && printf "\033&10H" && exit 0
exit 2
```
```

See the section on text filters earlier in this chapter for more information on how to install a text filter.

If your printer does not understand HP-PCL, you might be able to use the `tr` command to convert the LF into a CR/LF. A filter such as the following may do the trick:

```
```
#!/bin/sh
# Filter that fixes the stair stepping effect on non PCL printers.
/bin/cat | tr '\13' '\13\10' && exit 0
exit 2
```
```

Once again, see the section on text filters earlier in this chapter for more information on how to install a text filter.

# ### All the Text Prints on One Line, Creating a Mess and Writing Over the Top of Existing Text

This is basically the opposite of the stair-stepping problem. This problem is rare, but it does happen occasionally. Basically, the LF is being interpreted as a CR by the printer. The print head is getting returned to the beginning of the line, but the paper is not being advanced.