
These options are just the beginning; **pr** supports many more, which are described in its man page. As an example of **pr** in action, consider printing a double-spaced and numbered version of a configuration file (*say, /etc/profile*) for your reference. You can do this by piping together **cat** and its -n option to generate a numbered output, **pr** and its -d option to double-space the result, and |*pr* to print the file:

```
$ cat -n /etc/profile | pr -d | lpr
```

The result should be a printout that might be handy for taking notes on the configuration file. One caveat, though: If the file contains lines that approach or exceed 80 characters in length, the result can be single lines that spill across two lines. The result will be disrupted page boundaries. As a workaround, you can set a somewhat short page length with -l and use -f to ensure that the printer receives form feeds after each page:

```
$ cat -n /etc/profile | pr -df l 50 | lpr
```

![](img/f339a9f48c4b443e61c74acb4c9c3da4_86_0.png)

The **pr** command is built around assumptions about printer capabilities that were reasonable in the early 1980s. It’s still useful today, but you might prefer to look into GNU Enscript (*http://www.codeontio.com/people/mtr/genscript/*). This program has many of the same features as **pr**, but it generates PostScript output that can take better advantage of modern printer features.

## File-Viewing Commands

Sometimes you just want to view a file or part of a file. A few commands can help you accomplish this goal without loading the file into a full-fledged editor.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_86_1.png)

As described earlier, the **cat** command is also handy for viewing short files.

### Viewing the Starts of Files with head

Sometimes all you need to do is see the first few lines of a file. This may be enough to identify what a mystery file is, for instance; or you may want to see the first few entries of a log file to determine when the file was started. You can accomplish this goal with the **head** command, which echoes the first 10 lines of one or more files to standard output. (If you specify multiple filenames, each one’s output is preceded by a header to identify it.) You can modify the amount of information displayed by **head** in two ways:

- **Specify the number of bytes** The *-c num* or *--bytes=num* option tells **head** to display *num* bytes from the file rather than the default 10 lines.
- **Specify the number of lines** You can change the number of lines displayed with the *-n num* or *--lines=num* option.

### Viewing the Ends of Files with tail

The **tail** command works just like **head**, except that **tail** displays the *last* 10 lines of a file. (You can use the -c|--bytes and -n|--lines options to change the amount of data displayed, just as with **head**.) This command is useful for examining recent activity in log files or other files to which data may be appended.

The **tail** command supports several options that aren’t present in **head** and that enable the program to handle additional duties, including the following:

- **Track a file** The -f or --follow option tells **tail** to keep the file open and to display new lines as they’re added. This feature is helpful for tracking log files because it enables you to see changes as they’re added to the file.
- **Stop tracking on program termination** The -pid=pid option tells **tail** to terminate tracking (as initiated by -f or --follow) once the process with a process ID (PID) of *pid* terminates. (PIDs are described in more detail in Chapter 2, “Managing Software.”)

Some additional options provide more obscure capabilities. Consult **tail**’s man page for details.

### Paging Through Files with less

The **less** command’s name is a joke; it’s a reference to the **more** command, which was an early file pagers. The idea was to create a better version of **more**, so the developers called it **less**.

The idea behind **less** (and **more**, for that matter) is to enable you to read a file a screen at a time. When you type **less** *filename*, the program displays the first few lines of *filename*. You can then page back and forth through the file:

- Pressing the spacebar moves forward through the file a screen at a time.
- Pressing Esc followed by V moves backward through the file a screen at a time.
- The Up and Down arrow keys move up or down through the file a line at a time.
- You can search the file’s contents by pressing the slash (/) key followed by the search term. For instance, typing /portable finds the first occurrence of the string **portable** after the current position. Typing a slash followed by the Enter key moves to the next occurrence of the search term. Typing n alone repeats the search forward, while typing N alone repeats the search backward.
- You can search backward in the file by using the question mark (?) key rather than the slash key.
- You can move to a specific line by typing g followed by the line number, as in g50 to go to line 50.
- When you’re done, type q to exit from the program.

Unlike most of the programs described here, **less** can’t be readily used in a pipe, except as the final command in the pipe. In that role, though, **less** is very useful because it enables you to conveniently examine lengthy output.

## File-Summarizing Commands

The final text-filtering commands I describe are used to summarize text in one way or another. The `cut` command takes segments of an input file and sends them to standard output, while the `wc` command displays some basic statistics on the file.

### Extracting Text with cut

The `cut` command extracts portions of input lines and displays them on standard output. You can specify what to `cut` from input lines in several ways:

**By byte** The `-b *list*` or `--bytes=*list*` option cuts the specified list of bytes from the input file. (The format of a `list` is described shortly.)

**By character** The `-c *list*` or `--characters=*list*` option cuts the specified list of characters from the input file. In practice, this method and the by-byte method usually produce identical results. (If the input file uses a multi-byte encoding system, though, the results won’t be identical.)

**By field** The `-f *list*` or `--fields=*list*` option cuts the specified list of fields from the input file. By default, a field is a tab-delimited section of a line, but you can change the delimiting character with the `-d *char*`, `--delimiter=*char*` option, where `char` is the character you want to use to delimit fields. Ordinarily, `cut` echoes lines that don’t contain delimiters. Including the `-s` or `--only-delimited` option changes this behavior so that the program doesn’t echo lines that don’t contain the delimiter character.

Many of these options take a *list*, which is a way to specify multiple bytes, characters, or fields. You make this specification by number; it can be a single number (such as 4), a closed range of numbers (such as 2–4), or an open range of numbers (such as -4 or 4-). In this final case, all bytes, characters, or fields from the beginning of the line to the specified number or from the specified number to the end of the line are included in the list.

The `cut` command is frequently used in scripts to extract data from some other command’s output. For instance, suppose you’re writing a script and the script needs to know the hardware address of your Ethernet adapter. This information can be obtained from the `ifconfig` command (described in more detail in Chapter 8, “Configuring Basic Networking”):

```
$ ifconfig eth0
eth0      Link encap:Ethernet  HWaddr 00:0C:76:96:A3:73
          inet addr:192.168.1.3  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::20c:76ff:fe96:a373/64 Scope:Link
          UP BROADCAST NOTRAILERS RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:71273424  errors:0  dropped:0  overruns:0  frame:0
          TX packets:5273519  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:1000
          RX bytes:6272843708 (5982.2 Mb)  TX bytes:1082453585 (1032.3 Mb)
          Interrupt:10 Base address:0xde00
```

![](img/f339a9f48c4b443e61c74acb4c9c3da4_88_0.png)

Unfortunately, most of this information is extraneous for the desired purpose. The hardware address is the 6-byte hexadecimal number following `HWaddr`. To extract that data, you can combine `grep` (described shortly, in “Using `grep`”) with `cut` in a pipe:

```
$ ifconfig eth0 | grep 'HWaddr' | cut -d " " -f 11
00:0C:76:96:A3:73
```

Of course, in a script you would probably assign this value to a variable or otherwise process it through additional pipes. Chapter 9 describes scripts in more detail.

### Obtaining a Word Count with `wc`

The `wc` command produces a word count (that’s where it gets its name), as well as line and byte counts, for a file:

```
$ wc file.txt
308 2343 15534 file.txt
```

This file contains `308` lines (or, more precisely, `308` newline characters), `2,343` words; and `15,534` bytes. You can limit the output to the newline count, the word count, the byte count, or a character count with the `--lines` (`-l`), `--words` (`-w`), `--bytes` (`-c`), or `--chars` (`-m`) option, respectively. You can also learn the maximum line length with the `--max-line-length` (`-L`) option.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_89_0.png)

> For an ordinary ASCII file, the character and byte counts will be identical. These values may diverge for files that use multi-byte character encodings.
