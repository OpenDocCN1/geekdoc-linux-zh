# Searching and Interpreting Log Files

Most log files are simple text with variable data that can be read with your favorite paging application, such as `less`. Their value lies in the fact that they tend to be large with lots of different information. While it is both educational and beneficial to browse through them now and then to see what is happening on your computer, if you are searching for a specific type of event or troubleshooting a particular issue, all the other events will simply clutter and get in the way. There are several useful ways to deal with this, include `grep`, `tail`, `awk`, and `sed`.

# grep

The `grep` command is an all-around super handy search utility. You can pipe the output of a command into it, and use it to filter what shows up on the screen, or you can feed files directly to it, and it will spit out only the bits you are interested in. The syntax for `grep` is as follows:

```
grep [options] PATTERN [file]
```

Some helpful options are as follows:

+   - `-i` or `--ignore-case` to ignore the case of the text you are searching for.

+   - `-v` or `--invert-match` to only show lines that *don’t* contain the search pattern.

+   - `-c` or `--count` will only display the number of lines that match the `PATTERN`. Used with the `-v` option, it will show the number of lines that *don’t* match the `PATTERN`.

+   - `-r` or `--recursive` will search down through subdirectories.

+   - `-a NUM` or `--after-context = NUM` will include NUM number of lines after the matching line.

+   - `-b NUM` or `--before-context = NUM` will include NUM number of lines after the matching line.

The `before-context` and `after-context` options are handy to provide additional information before and after the matching line to give more data that may be associated with the specific event you are interested in.

One of the handy features of `grep` is that you don’t even have to know what file you want to search in:

```
cd /var/log
grep -i usb*
```