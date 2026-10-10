# **OPTIONS (CONT.)**

| Use This Option | To Do This |
| :--- | :--- |
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

# **EXAMPLES**

| This Command | Does the Following |
| :--- | :--- |
| cat example.ps \| lpr | Reads the specified file (example.ps) and sends the output to the default print spool. |
| pr database.txt \| lpr | Formats the specified file (database.txt) with page numbers and headers and sends the output to the default print spool. |

# **lprm**

lprm \[ option \] [-] job# \[ user \]

Removes job# from the printer queue. To determine the job number, use lpq -l.

*See also* lpr.