**od**

The `od` utility is used to dump the contents of a file and is useful for viewing files with non-printing characters such as binaries. By default, its output is in 2-byte octal numbers. Its syntax is

```
od [options] file
```

The output from a file might look like the following:

```
0000000 066101 064160 043141 066151 066145 071551 005164 064506
0000020 062554 064554 072163 061412 072141 027064 074164 005164
0000040 060544 031171 062012 074541 005103 064544 072143 063012
0000060 066151 071545 066412 073571 064550 064143 071412 063157
0000100 062164 074541 000012
0000105
```

In this example, the first column is the offset of each line and then each two bytes are represented by a three-digit, octal number.

**paste**

The `paste` utility joins the corresponding lines from the named files and sends the output to the display. The output separates the joined lines with a tab. Its syntax is

```
paste [options] filename
```

Use the `-d` option to have the joined lines separated by another character, rather than separating them with a tab.

You also can use the `-s` option. This causes `paste` to output one file followed by a newline character and then output the next file. With this option, the lines are not joined together but the files are pasted one after the other.

The `paste` utility often is used in conjunction with `cut` to rearrange columns. First, you would use `cut` to get each column in a separate file, and then use `paste` to join them in the order you want.

**pr**

The `pr` utility is used to break files into pages. Its syntax is

```
pr [options] file
```

The `pr` utility is most frequently used to send a file to a printer. The standard page length is 66 lines but can be changed with the `-l` option. You can use the `-f` option to generate a form feed at the end of each page, instead of filling the page with newline characters.