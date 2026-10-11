Perl inherits `stdin`, `stdout`, and `stderr` from the shell. Perl does not access these streams directly but gives them names called **filehandles**. Perl accesses the streams via the filehandle. The filehandle for *stdin* is called **STDIN**; the filehandle for *stdout* is called **STDOUT**; and the filehandle for *stderr* is called **STDERR**. STDERR is a separate stream that sends its output to the screen and allows you to redirect those errors to, for, example, an error log in order to find out what went wrong. Later, we’ll use Perl techniques to deal with errors and error messages. (See Figure 4.1.)

![](bbox=[0.19, 0.24, 0.77, 0.64])

**Figure 4.1** Reading from **STDIN** and writing to **STDOUT**.

In Chapter 10, "Getting a Handle on Files," we’ll see how you can create your own filehandles, but for now we’ll stick with those that are predefined.

The *print* and *printf* functions, by default, send their output to the **STDOUT** filehandle, your screen. For example:

```
```perl
print "Give me your name";
chomp($name = <STDIN>);
# User is prompted to enter something at the keyboard,
# until he presses the return key. The chomp function removes the newline.
if ( $name eq "" ) { print STDERR "You didn't enter anything.\n";
    exit 1; }
```
```