# PROCESSING TEXT FILES WITH sed 297

Listing 10.47 shows a brief sample application of sed. The command displays the currently running programs of the user. The first line normally consists of a heading that interferes with automatic processing. This line is not to be displayed. Then, the output of the ps command is redirected via a pipe to the sed editor. The sed command 1d means that the first line is be deleted.

```
(Linux):'$ ps | sed '1d'
95 p 1 SW      0:04 (bash)
11109 p 6 S       0:06 -bash
11110 p 5 SW      0:05 (bash)
11111 p b SW      0:04 (bash)
11811 p 5 S       2:02 emacs
12716 p 6 R       0:00 ps
12717 p 6 R       0:00 sed 1d
```

# Listing 10.47 A simple example of sed.

All sed consist of only one letter. Individual commands are separated by an end-of-line in the command file or by a semicolon. Each command can be associated to an address or an address range. The address can be specified by means line numbers – 1 in the above example – or by means of a search pattern (regular expression). The command is then executed for each line that matches the search criterion. The address specification is directly followed by the command, in the above example, the 'd' (delete) command. Some commands expect parameters, which are specified directly after the command in question.

sed processes the input line by line. If a command is to executed for a given line number, this number is specified in front of the command. It is also possible to specify a range of lines, with the first and the last line numbers of the range separated by comma. Examples of the use of line numbers are shown in Listing 10.48. The output of the commands is not printed here for reasons of space – we suggest that you just try out.

```
(Linux):> head /etc/services | sed -e '1d'
(Linux):> head /etc/services | sed -e '1,5d'
(Linux):> head /etc/services | sed -e 'Sd'
```

# Listing 10.48 Examples for the use of line numbers.

ps has an option (-h) for suppressing this line, but we will disregard it for the purpose of this example