# Part IV ♦ Running Applications

Groff macro packages are stored in /usr/share/groff*/tmac. The man macros are called from the an.tmac file, mm macros are from m.tmac, and we are from e.tmac. The naming convention for each macro package is xxx.tmac, where xxx represents the macro package. In each case, you can deduce the name of the macro package by adding an m to the beginning of the file prefix.

![](bbox=[0.133, 0.222, 0.169, 0.303])

Instead of noticing a specific macro package, you can use mandoc to choose one.

When you run the groff formatting command, you can indicate on the command line which packages you are using. You can also indicate that the command should run through any of the following commands that preprocess text for special formats:

+   - eqn— Formats macros that produce equations in groff.
- pic— Formats macros that create line drawings in groff.
- tbl— Formats macros that produce tables within groff.

The formatted Groff document is output for a particular device type. The device can be a printer, a window, or (for plain text) your shell. Here are the output formats:

+   - ps—PostScript for PostScript printer or a PostScript viewer
- lj4—Output for an HP LaserJet or other PCL5-compatible printer
- ascii—Plain-text output that can be viewed from a Terminal window
- dvi—Output in TeX dvi, to output to a variety of devices described later
- X75—Output for an X11 70 dots/inch preview
- X100—Output for an X11 100 dots/inch preview
- latin1—Typewriter-like output using the ISO Latin-1 character set

# Formatting and Documents with Groff

Try formatting and printing an existing Groff document using many pages from your system. You'll find some in /usr/share/man/*; they're compressed, so copy them to a temporary directory and unzip them to try out Groff.

The following commands copy the how man page to the /tmp directory, unzip it, and format it in plain text so you can page through it on your screen:

```
$ cp /usr/share/man/1/chown.1gz /tmp
$ gunzip /tmp/chown.1.gz | less
$ groff -Tascii -man /tmp/chown.1
```

In this example, the man page (chown.1.gz) is copied to the /tmp directory, unzipped (using gunzip), and output in plain text (-Tascii) using the man macros