# **OPTIONS**

| **Use This Option** | **To Do This** |
| --- | --- |
| `-c, --count` | Prefix lines by the number of occurrences |
| `-d, --repeated` | Print the duplicate lines but no unique lines |
| `-n f n, --skip-fields=n` | Skip the first *n* fields |
| `--help` | Show the available options |
| `-i, --ignore-case` | Ignore case |
| `-n` | Skip the first *n* lines |
| `+n, -s, --skip-chars=n` | Skip the first *n* characters |
| `-u, --unique` | Print only the unique lines but not duplicate ones |
| `--version` | Show the version number |
| `-W n --check-chars=n` | Compare only the first *n* characters per line |

# **EXAMPLE**

| **This Command** | **Does the Following** |
| --- | --- |
| `uniq dupes.txt nodupes.txt` | Removes the duplicate lines from `dupes.txt` (a sorted file) and writes to `nodupes.txt`. |

# **unstr**

unstr [ option ] [ *datafile* ] [ *output-file* ]

Reverses the work of *strfile* by printing out the stored strings in the data file to the output file.

*See also fortune.*