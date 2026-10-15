
no file is given, stdin is encoded. uudecode reads an encoded file, strips off any leading and trailing lines added by mailer programs, and re-creates the original binary data with the filename and the mode and owner specified in the header. The encoded file is an ordinary ASCII text file; it can be edited by any text editor. But it is best only to change the mode or file label in the header to avoid corrupting the decoded binary.

## EXAMPLE A.68

```
1  uuen code mybinfile decodedname > uumybinfile.tosend
2  uudecode uumybinfile.tosend
```

## EXPLANATION

- 1 The first argument, mybinfile, is the existing file to be encoded. The second argument is the name to be used for the uudecoded file, after mailing the file, and uumybinfile.tosend is the file that is sent through the mail.
- 2 This decodes the uuen coded file and creates a filename as given as the second argument to uuen code.

## wc—counts lines, words, and characters

```
wc [ -lwc ] [ filename ... ]
```

wc counts lines, words, and characters in a file or in the standard input if no filename is given. A word is a string of characters delimited by a space, tab, or newline.

## EXAMPLE A.69

```
1  wc filex
2  who | wc -l
3  wc -l filex
```

## EXPLANATION

- 1 Prints the number of lines, words, and characters in filex.
- 2 The output of the who command is piped to wc, displaying the number of lines counted.
- 3 Prints the number of lines in filex.

## what—extracts SCCS version information from a file by printing information found after the @(#) pattern

```
what [ -s] filename
```

what searches each filename for the occurrence of the pattern @(#), which the SCCS get command substitutes for the %Z keyword, and prints what follows up to a ">", newline, \, or null character.

## which—locates a command and displays its pathname or alias (UCB)

```
which [ filename ]
```

which takes a list of names and looks for the files that would be executed had the names been given as commands. Each argument is expanded if it is aliased, and searched for along the user's path. Both aliases and path are taken from the user's .cshrc file. Only .cshrc file is used.

## whereis—locates the binary, source, and manual page files for a command (UCB)

```
whereis [ -bmsu ] [ -BMS directory ... -f ] filename
```

## who—displays who is logged on the system

## write—writes a message to another user

```
write username [ ttyname ]
```

write copies lines from your terminal to another user's terminal.

## xargs—constructs an argument list(s) and executes a command

```
xargs [ flags ] [ command [ initial-arguments ] ]
```

xargs allows you to transfer contents of files into a command line and dynamically build command lines.

## EXAMPLE A.70

- 1 ls $1 | xargs -i -t mv $1/{ } $2/{ }
- 2 ls | xargs -p -I rm -rf

## EXPLANATION

- 1 Moves all files from directory $1 to directory $2, and echos each mv command just before executing.
- 2 Prompts (-p) the user which files are to be removed one at a time and removes each one.

## zcat—uncompresses a compressed file to standard output; Same as uncompress -c

```
zcat [ file ... ]
```

## EXAMPLE A.71

```
zcat book.doc.Z | more
```

## zipinfo—lists detailed information about a ZIP archive

```
zipinfo [-l2smVhMCTz] file[.zip][file(s)...] [-x xfile(s) ...]
```

zipinfo lists technical information about files in a ZIP archive, most commonly found on MS-DOS systems. Such information includes file access permissions, encryption status, type of compression, version and operating system or file system of compressing program, and the like. The default behavior (with no options) is to list single-line entries for each file in the archive, with header and trailer lines providing summary information for the entire archive. The format is a cross between UNIX ls -l and unzip -v output.

## zmore—file perusal filter for crt viewing of compressed text

```
zmore [ name ... ]
```

zmore is a filter which allows examination of compressed or plain text files one screenful at a time on a soft-copy terminal. zmore works on files compressed with compress, pack, or gzip, and also on uncompressed files. If a file does not exist, zmore looks for a file of the same name with the addition of a .gz, .z, or .Z suffix. Behaves like the more command, printing a screenful at a time.
