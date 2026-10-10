Use lptest to find job numbers. See “Reading the Status of a Printer Spool,” page 305.

# The lprm Command (Remove Print Jobs)

| Option | Action | Comments |
| :--- | :--- | :--- |
| -P PRINTER | Sets the printer to use | Not needed if the default is used. |
| -USER | Removes all jobs sent by the user specified. |  |

# Reading the Status of a Printer Spool

Type: lptest -t OPTIONS.

# Printing From the Command Line

Type: lpr OPTIONS FILES.

# The lpr Command (Print)

| Option | Action | Comments |
| :--- | :--- | :--- |
| -P PRINTER | Selects the printer to use. | Otherwise, the system default is used. |
| -S | Sends a symbolic link to the printer instead of the file. | This option saves time and disk space for large files, but may cause printing to be slower. |