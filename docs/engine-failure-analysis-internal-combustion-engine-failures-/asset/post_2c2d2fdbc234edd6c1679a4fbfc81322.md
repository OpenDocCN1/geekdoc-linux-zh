
## look

### EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| less magic.txt | Displays the specified file (magic.txt) in the less paging utility. |
| sort magic.txt \| less | Sorts the lines of the specified file (magic.txt) and displays the output on-screen. |
| pr magic.txt \| less | Formats the specified file (magic.txt) for printing and views the output on-screen. |

look [ option ] string [ filename ]

Displays lines in filename that begin with string. The file must be sorted. If you do not specify a filename, the utility uses the default ispell dictionary.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -a | Use the alternate dictionary |
| -d | Search alphanumeric characters only |
| -f | Ignore case |
| -t character | Stop searching the string at character |

### EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| look mus | Displays all the words in the default ispell dictionary that begin with mus. |
| look 'Secret #47' secrets.txt | Displays the line in secrets.txt that begins with Secret #47. |

## lpq

```
lpq [ option ] [ job# ] [ user ]
```

Reports the status of the printing queue. You can optionally specify the job number (with job#) and the user name.

See also lpr.

### OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -P *printer* | Use *printer* rather than the default |
| -l | List printer queue information |

### EXAMPLE

| This Command | Does the Following |
| --- | --- |
| lpq | Shows the status of the current print queue, including the job numbers of waiting jobs if there are any. |

## lpr

```
lpr [ option ] *filename*
```

Prints *filename*. Uses a print spooling daemon to store the files temporarily until the facilities become available.

### OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -#*n* | Print *n* copies |
| -C *string* | Print the specified string as the job classification on the burst page |
| -h | Suppress the printing of the burst page |
| -i\[ n\] | Indent by n columns |
| -J string | Use string as the job name on the burst page |
| -l | Allow printing of control characters |
| -m | Send mail upon completion |
| -P device | Use device for output |
| -P | Use pr to format the files |
| -r | Remove the file when printing is complete |
| -s | Create copies in the temporary directory using symbolic links |
| -T string | Use string as the title for pr output |
| -U user | Print the specified username on the burst page |
| -wn | Set the page width to n |

### EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| cat example.ps \| lpr | Reads the specified file (example.ps) and sends the output to the default print spool. |
| pr database.txt \| lpr | Formats the specified file (database.txt) with page numbers and headers and sends the output to the default print spool. |

## lprm

lprm [ option ] [-] job# [ user ]

Removes job# from the printer queue. To determine the job number, use lpq -l.

*See also* lpr.

### OPTIONS

| Use This Option | To Do This |
|---|---|
| -P *printer* | Use the specified printer queue rather than the default. |
| - | Remove all of the user's print jobs. |

## md5sum

```
md5sum [ option ] [ *filename* ]
```

Displays or checks an MD5 checksum on the specified *filename*. When used without an argument, this utility reads from the standard input.

### OPTIONS

| Use This Option | To Do This |
|---|---|
| -b, --binary | Read the file in binary mode. |
| -c, --check | Check MD5 sums against the list given in *filename*. |
| -t, --text | Read files in text mode. This is the default. |
| --help | Display available options. |
| --version | Show the version number. |

## more

```
more [ option ] [ *filename* ]
```

Displays *filename* on-screen and enables you to page through it easily. You can specify more than one *filename* in a space-separated list or by using a shell pattern (see the section “Shell Patterns” in Chapter 4). In the interactive mode, you can use the commands listed in the Commands table in this section.

See also *less*.

### OPTIONS

| Use This Option | To Do This |
|---|---|
| -n | Use a screen size of n lines |
| +/ | Specify a search string |
| +n | Start at line number n |
| -c | Paint screen from the top rather than scrolling |
| -d | When an illegal key is pressed, prompt the user with the message "[Press space to continue, 'q' to quit.' and '[Press 'h' for instructions.]" |
| -f | Count actual (unfolded) lines rather than screen lines |
| -I | Prevent pauses after encountering a form feed character (^I) |
| -P | Clear the whole screen and display the text instead of scrolling |
| -s | Squeeze multiple blank lines into one |
| -u | Suppress underlining |

### COMMANDS

| Use This Command | To Do This |
|---|---|
| h, ? | Display a summary of these commands. If you forget all the other commands, remember this one. |
| !<cmd> , :! <cmd> | Execute <cmd> in a subshell. |
| = | Display the current line number. |
| Ctrl+L | Redraw the screen. |
| ' | Go to the place where the previous search started. |
| . | Repeat the previous command. |
| [ n ] /regexp | Search for the nth occurrence of regexp, a regular expression. The default occurrence is 1. |
| :f | Display the current filename and line number. |
| [ n ] :n | Go to nth next file. The default setting for n is 1. |
| [ n ] :p | Go to nth previous file. The default setting for n is 1. |
| `[ n] b, [ n] Ctrl + B` | Go back $n$ screenfuls of text. The default setting for $n$ is 1. |
| `[ n] d, [ n] Ctrl +D` | Scroll $n$ lines. The default is the current scroll size, which is initially 11. If you specify a different scroll size, it becomes the new current scroll size. |
| `[ n] f` | Skip forward $n$ screenfuls of text. The default setting for $n$ is 1. |
| `[ n] n` | Search for the $n$th occurrence of the last regular expression you searched for. The default setting for $n$ is 1. |
| `q, Q` | Exit. |
| `[ n] Enter` | Display the next $n$ lines of text. Defaults to 1. The argument becomes the new default. |
| `[ n] s` | Skip forward $n$ lines of text. Defaults to 1. |
| `[ n] Spacebar` | Display the next $n$ lines of text. Defaults to the current screen size. |
| `v` | Start up /usr/bin/vi at the current line. |
| `[ n] z` | Display the next $n$ lines of text. Defaults to the current screen size. The argument becomes the new default. |

### EXAMPLES

| This Command | Does the Following |
|---|---|
| `more magic.txt` | Displays the specified file (magic.txt) in the less paging utility. |
| `sort magic.txt | more` | Sorts the lines of the specified file (magic.txt) and displays the output on-screen. |
| `pr magic.txt | more` | Formats the specified file (magic.txt) for printing and views the output on-screen. |

## nl

```
nl [ option ] [ filename ]
```

Numbers the lines of filename. You can specify more than one filename in a space-separated list or by using a shell pattern (see the section "Shell Patterns" in Chapter 4). By default, the utility writes to standard output. Use output redirection to save the output to a file. If you do not specify a filename, the utility accepts input from the standard input.

### OPTIONS

| Use This Option | To Do This |
|---|---|
| -b style, -body-numbering=style | Use style for numbering body lines. (See the Styles table in this section.) |
| -d style, -section-delimiter=charchar | Use charchar (two characters) for separating logical pages. |
| -f style, -footer-numbering=style | Use style for numbering footer lines. (See the Styles table in this section.) |
| -h style, -header-numbering=style | Use style for numbering header lines. (See the Styles table in this section.) |
| --help | Display the available options. |
| -i n, -page-increment=n | Use the line number increment specified by n. |
| -l n, -join-blank-lines=n | Count n empty lines as one. |
| -n format, -number-format=format | Insert line numbers according to the specified format. |
| -p, -no-renumber | Do not reset line numbers at logical pages. |
| -s, -number-separator=string | Use string as a number separator. |
| -v, -first-page=n | Use n as the first line number for each logical page. |
| --version | Show the version number. |
| -w, -number-width=n | Use n columns for line numbers. |
