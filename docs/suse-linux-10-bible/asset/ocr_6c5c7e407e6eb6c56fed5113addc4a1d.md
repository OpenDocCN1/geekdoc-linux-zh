# Chapter 8 ♦ The X Window System 217

![](bbox=[0.188, 0.125, 0.811, 0.497])

Figure 8-8: Fluxbox

The first step in building and installing any X application is to obtain its source code. The source code for the latest version of Fluxbox is always available from the Fluxbox's site page, which is located at www.fluxbox.org/download.php. The version of Fluxbox we used in the rest of this section is 0.9.13, which was available from http://downloads.sourceforge.net/fluxbox/fluxbox-0.9.13.tar.gz at the time this book was updated.

After downloading the source code, you must unpack the archive using the standard Linux command, as in the following example:

```
$ tar xzf fluxbox-0.9.13.tar.gz
```

This will create a directory named Fluxbox-0.9.13 in the current directory. Use the cd command to change to this directory, and run the configuration script provided with Fluxbox by executing the command, ./configure. (The ./ prefix ensures that the shell runs the script that is found in the current directory.) This will produce very verbose output as it explores your system to ensure that all of the correct components for compilation are present on your system and constructs a Makefile that you can use to build Fluxbox. The following is some sample output from the configure script: