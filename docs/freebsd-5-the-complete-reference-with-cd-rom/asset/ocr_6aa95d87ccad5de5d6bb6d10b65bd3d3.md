the file is plain text; if you try to print a binary file, such as a graphics file, the script will fail.)

# **Note**

> Listing 9-2 is useful only if your printer is a PostScript model, although you could adapt it for other printer types by altering it to pass a PostScript file through Ghostscript and not use nenscript on plain text files.

# listing 9-2
A Simple
nput Filter

```
```bash
#!/bin/sh
# Check to see if input is PostScript. If not, pass through
# nenscript

read firstline
firstchars=`expr "$firstline" : '(\\.\\.)'`

if [ "$firstchars" = "%!" ]
then
# PostScript file; pass through $firstline & rest of file
echo "$firstline" & cat & printf "\\004"
exit 0
else
# Not PostScript; use nenscript to process
(echo "$firstline"; cat) | /usr/local/bin/nenscript -p \\
& printf "\\004"
exit 0
fi
```
```

# **Caution**

> The Listing 9-2 line that begins firstchars= includes two types of single quotes. The outermost pair are backquotes, which are found to the left of the \ key on most keyboards, sharing the key with the tilde (~). The innermost pair are ordinary single quotes, which appear to the left of the ENTER key on most keyboards. Be sure to use the correct quote type. This line also includes a pair of double quotes, so be sure to use those appropriately, as well.

Listing 9-2 does several things. Although explaining every line is beyond the scope of this chapter, a basic understanding of this script is useful. The script expects to receive a file on standard input, and sends a file to standard output. The read firstline line reads the first line of the input file into a variable called $firstline. The next line extracts the first two characters of this line into a variable called $firstchars. The if line checks to see if these characters identify the file as a PostScript file. If they do, the script echoes $firstline and the rest of the file, passing it through unchanged. If the first two characters don't identify the file as a PostScript file, the script sends the file through the nenscript program, which converts plain text to PostScript.