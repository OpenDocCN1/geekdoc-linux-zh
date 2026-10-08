# Advanced Bash-Scripting Guide

```
echo "eval($var / 3)" | m4      # 33
exit
```

xmessage
This X-Based variant of echo pops up a message/query over the desktop.

```
xmessage Left click to continue -button okay
```

zenity
The zenity utility is adept at displaying GTK+ dialog widgets and very suitable for scripting purposes.
doeexec
The doexec command enables passing an arbitrary list of arguments to a binary executable. In
particular, passing argv[0] (which corresponds to $0 in a script) lets it be invoked by
various names, and it can then carry different sets of actions, according to the name by which it
was called. This is somewhat roundabout of passing options to an executable.

For example, the /usr/local/bin directory may contain a binary called "aaa". Invoking doexec
usr/local/aaa list would list all those files in the current working directory with an "aaa",
whoking (the same executable) doexec/usr/local/bin/aaa delete delete those files.

+   The behaviors of the executable can be defined within the code of the
executable itself, analogous to something like the following in a shell script:

```
case basename $0 in
  *name1* ) do_something;
  *name2* ) do_something_else;
  *name3* ) do_yet_another_thing;
  ) bail_out;
esac
```

dialog
The dialog family provides a method of calling interactive "dialog" boxes from a script. The
more elaborate variations of dialog -- ddialog, Xdialog, and kdialog -- actually invoke X-Windows
widgets.

sox
The sox, or "sound exchange" command plays and performs transformations on sound files. In fact,
/usr/bin/play executable (now deprecated) is nothing but a shell wrapper for sox.

For example, sooundfile.wav soundfile.au changes a WAV sound file into a (Sun audio format)
AU sound file.

Shell scripts are ideally suited for batch-processing sox operations on sound files. For examples, 
the Linux Radio Timeshift HOWTO and the MP3do Project.