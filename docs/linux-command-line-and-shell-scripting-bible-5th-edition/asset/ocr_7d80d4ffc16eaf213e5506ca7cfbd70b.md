**Table 4.6 Continued**

| Single Dash | Double Dash | Description |
| :--- | :--- | :--- |
| -g | `--general-numeric-sort` | Use general numerical value to sort. |
| -i | `--ignore-nonprinting` | Ignore nonprintable characters in the sort. |
| -k | `--key=POS1[,POS2]` | Sort based on position POS1 and end at POS2 if specified. |
| -M | `--month-sort` | Sort by month order using three-character month names. |
| -m | `--merge` | Merge two already sorted data files. |
| -n | `--numeric-sort` | Sort by string numerical value. |
| -o | `--output=file` | Write results to the specified file. |
| -R | `--random-sort` | Sort by a random hash of keys. |
| | `--random-source=FILE` | Specify the file for random bytes used by the -R parameter. |
| -r | `--reverse` | Reverse the sort order (descending instead of ascending). |
| -S | `--buffer-size=SIZE` | Specify the amount of memory to use. |
| -s | `--stable` | Disable last-resort comparison. |
| -T | `--temporary-directory=DIR` | Specify a location to store temporary working files. |
| -t | `--field-separator=SEP` | Specify the character used to distinguish key positions. |
| -u | `--unique` | With the -c parameter, check for strict ordering; without the -c parameter, output only the first occurrence of two similar lines. |
| -z | `--zero-terminated` | End all lines with a NULL character instead of a new line. |

The `-k` and `-t` parameters are handy when sorting data that uses fields, such as the `/etc/passwd` file. The `-r` option also sorts the values in descending order so that you can easily see what files are taking up the most space in your directory.

# ### Searching for data

Often in a large file, you have to look for a specific line of data buried somewhere in the middle of the file. Instead of manually scrolling through the entire file, you can let the `grep` command search for you. The command-line format for the `grep` command is `grep [options] pattern [file]`