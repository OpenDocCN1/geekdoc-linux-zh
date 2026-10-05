7. Use visual block mode to remove the time column, leaving the month and day on all lines.

Use the arrow keys to position the cursor at the first character. Enter visual block mode using
Ctrl+V. Use the arrow keys to position the cursor at the last character and last row of the
column. Delete the selection with x.

```
student@workstation~
File Edit View Search Terminal Help
-rw 1 student 183 Jan 21 15:00 .bash_history
-rw 1 student 141 Oct 12 23:56 .bash_log
-rw 1 student 141 Oct 12 23:56 .bash_profile
-rw 1 student 128 Dec 12 20:33 .cache
-drwx 2 student 201 Jan 24 14:00 Desktop
-drwx 2 student 256 Jan 06 14:16 Documents
-drwx 2 student 256 Jan 06 14:16 Downloads
-drwx 2 student 256 Jan 06 14:16 Pictures
-rw 1 student 506 Jan 16 14:15 .editing_final_lab.txt
-rw 1 student 161 Jan 16 14:15 .esdt
-drwx 2 student 201 Jan 19 14:16 .fauthority
-drwx 2 student 256 Jan 06 14:16 Music
-drwx 2 student 256 Jan 06 14:16 Public
-drwx 2 student 256 Jan 06 14:16 Templates
-drwx 2 student 256 Jan 06 14:16 Video
-rw 1 student 1095 Jan 14 15:14 .viminfo
```

8. Remove the Desktop and Public rows. Enter visual line mode with uppercase V.

Use the arrow keys to position the cursor at any character on the Desktop row. Enter visual
mode with uppercase V. The full line is selected. Repeat for the
Public row.

```
student@workstation~
File Edit View Search Terminal Help
-rw 1 student 310 Jan 21 .bash_history
-rw 1 student 141 Oct 12 .bash_log
-rw 1 student 141 Oct 12 .bash_profile
-drwx 2 student 201 Jan 24 .cache
-drwx 2 student 201 Jan 24 Desktop
-drwx 2 student 256 Jan 06 .Documents
-drwx 2 student 256 Jan 06 .Downloads
-rw 1 student 926 Jan 22 .editing_final_lab.txt
-rw 1 student 161 Jan 14 .ICEauthority
-rw 1 student 318 Jan 14 .viminfo
-drwx 2 student 256 Jan 06 .Music
-drwx 2 student 256 Jan 06 .Pictures
-drwx 2 student 256 Jan 06 .Public
-drwx 2 student 734 Jan 04 .ps3
-drwx 2 student 256 Jan 06 .Templates
-rw 1 student 1095 Jan 14 .viminfo
```