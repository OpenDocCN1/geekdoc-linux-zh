# TABLE 10.3: LP requests LOG FILE CODES

| Code | Description |
| :--- | :--- |
| `=` | A separator line that is followed by the following pieces of information in a comma-delimited list: request ID, user identification (UID), group identification (GID), byte size in the unfiltered file, and the time the request was generated. |
| `C` | Number of copies printed. |
| `D` | Printer class or any printer. |
| `f` | Name of form used. |
| `F` | The print filename list in the order that it was printed. |
| `H` | Used to specify the handling characteristic: *resume*, *hold*, or *immediate*. |
| `N` | The alert used when a print request is successfully executed. **M** is used for e-mail alerts, and **W** is used when a message is sent to the console. |
| `O` | Used to specify the `¬o` options used by the `1p` command. |
| `p` | A list of the pages that were printed. |
| `P` | The print request priority that was used for printing. |
| `r` | Used to specify whether the file was output as a raw file using the `¬r` option of the `1p` command. Raw output is sent to the printer directly. |
| `s` | The request outcome in hexadecimal form. Among the output you see are `0x0004` (slow filtering completed), `0x0010` (printing completed), `0x0040` (print request cancelled), and `0x0100` (print request failed either conversion through the print filter or print execution from the print queue). |
| `S` | The name of the print wheel, cartridge, or character set that was used. |
| `t` | The type of content in the file(s) printed. |
| `T` | The title that is added to the banner page. |
| `U` | The name of the user who specified the print job. |
| `x` | Used to indicate that the slow filter was used for the print request. |
| `Y` | A list of the special modes that are communicated to the print filters. |
| `z` | The printer used in the request. |

You would use the `/var/1p/logs` directory to read information about specific jobs that have already executed from the print queue. The logs directory contains `request. n` files that are copies of logs from previous days. The `1p` cron job stores log files from two previous days, the `.1` and `.2` file suffixes.

# Print Filters

Print filters are translation routines that convert the output of a print file into the data that a printer needs to have in order to control the various printer elements. In a