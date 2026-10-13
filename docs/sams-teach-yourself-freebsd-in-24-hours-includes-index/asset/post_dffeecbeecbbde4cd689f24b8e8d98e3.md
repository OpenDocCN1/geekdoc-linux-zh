
## Configuring a Text Filter

We briefly mentioned filters earlier in the hour. Basically, they are where the majority of the printing work is actually done. All data being sent to the printer passes through a filter first. The filter can do such things as convert the data from one format into a different one that the printer can understand.

At a bare minimum, you will need a text filter. A text filter, as the name implies, is the filter used when the printer daemon receives simple plain text. Often times, the text filter is nothing more than a pass-through system that simply passes the raw data to the printer without doing anything to it. However, it can be as complex as a system that changes the data to a completely different format. (Later on, we will look at why you might need to change plain text to a completely different format.)

Text filters can either be written by you or installed as a program that someone else has written. Before you panic at the idea of writing your own filter, basic filters are easy to write. For example, if your printer can receive raw text data and print it fine without making any changes to it, the following filter can simply be written in a text editor and saved to a file. It might be all that you need:

```sh
#!/bin/sh
/bin/cat && exit 0
exit 2
```

The preceding program is what is known as a shell script. The details of writing shell scripts are beyond the scope of this book, but we will cover enough of the basics for you to understand what the preceding filter does.

The first line simply tells the shell which program it should use to interpret the rest of this file. In this case, it tells the shell that this file is a shell script and should be interpreted using the shell.

The second line executes the cat program. Basically, in its simplest form, cat takes whatever it receives on STDIN (which is normally the keyboard) and echoes it to STDOUT (which is normally the screen). How does this help us with printing? Because for printing, STDIN and STDOUT are redirected. In this case, STDIN is the print data being sent from the spooler, and STDOUT is the printer port that the printer is connected to. So in this case, the cat program simply takes whatever it receives from the print spooler and echoes it to the printer port.

The second part of the line, && exit 0, is a shorthand notation of saying basically, “Perform the exit 0 command if, and only if, the /bin/cat command completes successfully.” If cat does complete successfully, the shell script will exit with a status of 0 (which indicates a successful execution of the command) and the third line of the script will not be executed because the exit command on line 2 will take effect.

If on the other hand, the cat command fails (for whatever reason, it can't send the data to the port or some other such error), the exit 0 command on line 2 will not be executed (because the "if and only if" test fails). In this case, line 3 will be executed, which causes the shell script to exit with a status of 2. (Why exit status 2? Because lpd reads the exit status of the filter. A status code of 2 indicates that the filter failed with an unrecoverable error, and therefore informs lpd that it should not attempt to print the job again.)

The filter can be named anything you want. In this case, we will assume that it is named if-text. By convention, print filters are stored in /usr/local/libexec. When you have saved the file, you need to make it executable so that the lpd program can run it. The following command is an example:

```
chmod 555 /usr/local/libexec/if-text
```

A simple filter such as this should work fine for printing plain text on most non-Postscript printers. However, Postscript printers can't handle plain text. If you have a Postscript printer, you will need a slightly more complex setup that can convert the plain text into Postscript. This is covered in the following section.

## Formatting Plain Text for Postscript Printers

Postscript is a programming language for formatting text and graphics. It is device independent so that any printer that understands PostScript can print a PostScript document with no special drivers. PostScript is so common in the UNIX world that most UNIX applications can print PostScript output. Because of this, PostScript can be a very useful thing for your printer to have. However, one problem with PostScript printers is that they generally expect that everything they receive will be in PostScript format. As a result, you can't send plain text data directly to a PostScript printer. Plain text must first be run through a filter that can convert the plain text to PostScript.

The program a2ps, which is available in the print directory of the FreeBSD ports collection, is designed to do just that. After you have installed a2ps, you need to write a filter that can recognize if it is receiving PostScript or plain text, and then take the appropriate action. (Either send the data directly to the printer if it is already in PostScript format, or convert the data to PostScript and then send it to the printer if it is plain text.) Listing 9.1 is a sample filter that will do this.

### LISTING 9.1 A Sample Text Filter for PostScript Printers

```sh
#!/bin/sh
# Simple filter for PostScript printers

read header
ps_test=`expr "$header" : '\(..\)'`
if [ "$header" = "%!" ]
then
  # File is PostScript. Print pass through.
  echo "$header" && cat && printf "\004" && exit 0
  exit 2
else
  # File is plain text. Convert it first.
  (echo "$header"; cat) | /usr/local/bin/a2ps && printf "\004" && exit 0
  exit 2
fi
```

Like the previous filter, this file should be saved in /usr/local/libexec. The name if-ps might be a good choice. Also, remember once again to set the file to executable so that lpd can run it. You can use the following command to do this:

```
chmod 555 /usr/local/libexec/if-ps
```

We aren't going to go into detail about what this script does, but in a nutshell, it checks to see if the first two characters of the file are %!. (PostScript files start with these two characters.) If they are, the filter assumes that the file is PostScript, and it gets passed directly to the printer. If they are not, the filter assumes the file is plain text, and the data is passed through the a2ps program to be converted to PostScript before being sent to the printer.

Of course, if you don't have a PostScript printer, you might have the opposite problem. In other words, you need to print a PostScript document on a printer that doesn't understand PostScript. In this case, you can use a program called Ghostscript, which converts PostScript into a format that your printer can understand.

## Configuring a Ghostscript Filter

As mentioned previously, most UNIX applications can output PostScript. Although some UNIX applications contain print drivers for various printers, most of them do not. Instead, they just output PostScript. Use the Ghostscript program, which is available in the FreeBSD ports collection under the print directory, for converting the PostScript

Ghostscript supports a lot of printers. A list (which might not be complete) of supported printers is available at www.cs.wisc.edu/~ghost/doc/printer.htm.

The filter script for this is similar to the script for printing plain text on a PostScript printer—except that this time, the operations are reversed. This time, if the filter receives plain text, the text should be passed straight through without any formatting. On the other hand, if the filter receives PostScript, it should be sent to the Ghostscript program for conversion into an understandable format for your printer.

The following script, taken from the FreeBSD handbook, works for an HP Deskjet 500 (which cannot print PostScript directly).

```bash
#!/bin/sh
#
# ifhp - Print Ghostscript-simulated PostScript on a DeskJet 500
# Installed in /usr/local/libexec/hpif
#
# Treat LF as CR+LF:
#
printf '\033&k2G' || exit 2
#
# Read first two characters of the file
#
read first_line
first_two_chars=`expr "$first_line" : '\(..\)'`

if [ "$first_two_chars" = "%!" ]; then
# It is PostScript; use Ghostscript to scan-convert and print it.
#
# Note that PostScript files are actually interpreted programs,
# and those programs are allowed to write to stdout, which will
# mess up the printed output. So, we redirect stdout to stderr
# and then make descriptor 3 go to stdout, and have Ghostscript
# write its output there. Exercise for the clever reader:
# capture the stderr output from Ghostscript and mail it back to
# the user originating the print job.

exec 3>&1 1>&2
/usr/local/bin/gs -dSAFER -dNOPAUSE -q -sDEVICE=djet500 \
-sOutputFile=/dev/fd/3 && exit 0
#
/usr/local/bin/gs -dSAFER -dNOPAUSE -q -sDEVICE=djet500 \
-sOutputFile=... \
&& exit 0
else
```
