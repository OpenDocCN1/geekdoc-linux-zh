# Number (Continued)

| | |
| 1000 | Sticky bit |
| 0400 | Owner can read the file |
| 0200 | Owner can write to the file |
| 0100 | Owner can execute the file |
| 0040 | Group can read the file |
| 0020 | Group can write to the file |
| 0010 | Group can execute the file |
| 0004 | Others can read the file |
| 0002 | Others can write to the file |
| 0001 | Others can execute the file |

Table III-6 lists some typical modes.

# Example Modes

| | |
| 0777 | Owner, group, and public can read, write, and execute file. |
| 0755 | Owner can read, write, and execute; group and public can read and execute file. |
| 0711 | Owner can read, write, and execute; group and public can execute file. |
| 0644 | Owner can read and write; group can read the file. |
| 0640 | Owner can read and write, group can read, and public has no access to file. |