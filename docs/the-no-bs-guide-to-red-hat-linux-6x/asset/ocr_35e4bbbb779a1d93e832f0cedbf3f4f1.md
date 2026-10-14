| DOS | UNIX | DESCRIPTION |
|---|---|---|
| del
`del panda.zip` | rm
`rm panda.zip` | Remove a file. |
| edit
`edit panda.txt` | pico
`pico panda.txt` | Edit a text file. |
| fdisk
`fdisk` | fdisk
`fdisk /dev/hda` | Define disk partitions. |
| format
`format c:` | mk2fs
`mk2fs /dev/hda2` | Format a file system or disk. |
| find
`find /i "widget" *.txt` | grep
`grep -i "widget" *.txt` | Search for text within files. |
| help
`help find` | man
`man grep` | Display help for commands. |
| md
`md \newdir` | mkdir
`mkdir /newdir` | Make a new directory. |
| mode/ctty
`mode CON LINES=43` | stty
`stty rows=43` | Set modes on console or serial and/or printer port. |
| more
`more outlist.txt` | more
`more outlist.txt` | Display output screen by screen. |
| print
`print autoexec.bat` | lpr
`lpr .profile` | Print a file. |
| rename
`rename big.txt large.txt` | mv
`mv big.txt large.txt` | Move or rename a file. |
| rmdir
`rmdir \temp` | rmdir
`rmdir /home/temp` | Remove a directory. |
| scandisk
`scandisk c: /AUTOFIX` | e2fsck
`e2fsck -p /dev/hda2` | Check file system and fix errors. |
| sort
`sort /+6 < number.fil` | sort
`sort -k 6,7 number.fil` | Sort a file. |
| type
`type ascii.txt` | cat
`cat ascii.txt` | Display a file on the screen. |
| xcopy
`xcopy /s *.ps c:\tmp` | cp -r
`cp -x *.ps c:\` | Copy files and directories recursively. |