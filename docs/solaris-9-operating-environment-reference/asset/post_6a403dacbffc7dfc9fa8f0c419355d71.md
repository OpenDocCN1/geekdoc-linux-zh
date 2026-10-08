
# 1082

# ppgsz — Set Preferred Stack and/or Heap Page Size

# Synopsis

```
/usr/bin/ppgsz [-F] -o option,[option] cmd -p pid... 
```

# Use

Use the ppgsz command, new in the Solaris 9 Operating Environment, to set the preferred stack and/or heap page size for the target process(es), that is, the launched cmd or the process(es) in the pid list. ppgsz stops the process(es) while changing the page size. See memcntl(2).

Because of resource constraints, setting the preferred page size does not necessarily guarantee that the target process(es) gets the preferred page size. Use pmap(1) to view the actual heap and stack page sizes of the target(es). See pmap -s.

You must map large pages at addresses that are multiples of the size of the large page. Given that the heap is typically not large-page aligned, the starting portions of the heap (below the first page aligned address) are mapped to the system memory page size. See getpagesize(3).

# Options

- -F Preferred page page size for target process(es) even if controlled by other process(es). Exercise caution when using the -p option. See proc(1).

- -p Set the preferred page size option(s) for the target process(es) in the process-ID (pid) list following the -p option. The pid list can also consist of names in the /proc directory. Only the process owner or superuser is permitted to set page size.

cmd is interpreted if you do not specify -p. ppgsz launches cmd and applies page size option(s) to the new process.
The heap and stack preferred page sizes are inherited. Child process(es) created (fork(2)) from the launched process inherit the preferred heap and stack page sizes. The preferred page sizes are set back to the default system page size (see getpagesize(3)) on exec(1) (see exec(2)).

- -o option,[option] You must specify at least one of the following options

- - heap=size Specify the preferred page size for the heap of the target process(es), heap is defined to be the bss (uninitialized data) and the brk area that immediately follows the bss (see brk(2)). The preferred heap page size is set for the existing heap and for any additional heap memory allocated in the future.

- - stack_size Specify the preferred page size for the stack of the process(es). The preferred stack page size is set for the existing stack and newly allocated parts of the stack as it expands.
size must be a supported page size (see pagesize(1)) or 0, in which case the system selects an appropriate page size (see memcntl(2)). size defaults to bytes and can be specified in octal (0o), decimal, or hexadecimal (0xl). You can qualify the numeric value with K, M, G, or T to specify kilobytes, megabytes, gigabytes or terabytes. For example, you specify 4 Megabytes as 4194304. 0x400000, 0x1000K, or 4M.

# Examples

The following example sets the preferred heap page size to 4M and the preferred stack page size to 512K for all ora-owned processes commands that begin with ora.
example% ppgsz -o heap=4M, stack=512K -p `pgrep -u ora ^ora`

# Exit Status

- 0
Successful operation.
- non-zero
An error occurred.

# Files

```
/proc/*    Process files.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNmesu (32 bit) SUNmesxu (64 bit) |
| Interface Stability | Evolving |

# See Also

```
pagesize(1), pgrep(1), pmap(1), proc(1), brk(2), exec(2), fork(2),
memcntl(2), sbrk(2), getpagesize(3), proc(4), attributes(5)
```

# 1084

# pr

# pr - Print Files

# Synopsis

```
/usr/bin/pr [+page] [-column] [-adFmrt] [-e[char] [gap] [-h header]
[-i[char] [gap]] [-1 lines] [-n[char] [width]] [-o offset] [-s[char]]
[-w width] [-file...]
/usr/xpg4/bin/pr [+page] [-column -c column] [-adFmrt] [-e[char]
[gap]] [-h header] [-i[char] [gap]] [-1 lines] [-n[char] [width]]
[-o offset [-s[char]] [-w width] [-file...]
```

The pr command is a printing and pagination filter. If you specify multiple input files, each is read, formatted, and written to standard output. By default, the output is separated from 66-line pages, each with

- * A 5-line header that includes the page number, date, time, and the path name of the file.
- A 5-line trainer consisting of blank lines.

If standard output is associated with a terminal, diagnostic messages are deferred until the pr command has completed processing.
When you specify options for multicolumn output, output columns are of equal width; input lines that do not fit into a text column are truncated. By default, text columns are separated with one blank character.

# Options

In the following option descriptions, column, lines, offset, page, and width are positive decimal integers; gap is a nonnegative decimal integer. Some of the arguments are optional, and some of the arguments cannot be specified as arguments in the preceding option letter. In particular, the -s option requires you to keep the option letter with its argument, and the options -e, -i, and -n require that both arguments, if present, be kept with the option letter.

The following options are supported for both /usr/bin/pr and /usr/xpg4/bin/pr.

- -page Begin output at number page of the formatted output.

- -column Produce multicolumn output that is arranged in columns (default is 1) and is written down each column in the order in which the text is received from the input file. Do not use this with -m. The -e and -i options are assumed for multiple text-column output. Whether text columns are produced with identical vertical lengths is unspecified, but a text column never exceeds the length of the page (the -1 option). When used with -t, use the minimum number of lines to write output.

Modify the -column option so that the columns are filled across the page in a round-robin order (for example, when column is 2, the first input line heads column 1, the second heads column 2, the third is the second line in column 1, and so forth).

- -a Produce output double spaced; append an extra newline character following every newline found in the input.

- -e[char] [gap]

Expand each Tab character to the next greater column position specified by the formula n *gap+1, where n is an integer >0. If gap is omitted or it is 0, it defaults to 8. Expand all Tab characters in the input into the appropriate number of space characters. If nondigit character, char is specified, use it as the input Tab character.

- -f

Use a feedcharacter for new pages instead of the default behavior that uses a sequence of newline characters. Pause before beginning the first page if the standard output is associated with a terminal.

- -h header

Use the string header to replace the contents of the file header.

- -l lines

Override the 66-line default, and reset the page length to lines. Lines is not greater than the sum of both the header and trailer (in lines), suppress the header and trailer, as if the -t option were in effect.

- -m Merge files. Standard output to write one line from each file, side by side, into text columns of fixed width. Implementations merging of least nine lines.

- -n[char] [width]

Provide width-digit line numbering (for width is 5). The number occupies the first width positions of each text column of default output or each line of m output. If you specify char(any nondigit character), append to the line number to separate it from whatever follows (default for char is a Tab character).

- -o offset

Precede each line of output by offset spaces. If you do not specify the -option, the default offset is 0. The space is in addition to the output line width (see -w option).

- -p

Pause before beginning each page if the standard output is directed to a terminal (write an ALERT character to standard error and wait for a Return character to be read on /dev/tty).

- -r

Write no diagnostic reports on failure to open files.

- -s[char]

Separate text columns by the single character char instead of the appropriate number of space characters (default for char is the Tab character).

- -t

Write the 5-line identifying header nor the 5-line trailer usually supplied for each page. Quitting after the last line of each file without spacing to the end of the page.

- -w width

Set the width of the line to widthcolumn positions for multiple text-column output only. If you do not specify the -w or -s options, the default width is 72. If you do not specify the -option and specify the -s option, the default width is 512. For single column output, input lines are not truncated.
