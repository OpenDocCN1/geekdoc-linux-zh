# Determining Disk Usage with du

Another piece of information that you can access is how much disk space within the Unix system is in use. You can do so using du, as shown in Code Listing 7.5:

# To determine disk usage with du:

+   - du

At the shell prompt, enter du. As Code Listing 7.5 shows, you’ll get information about disk usage in the current directory as well as in all subdirectories. The numbers are usually measured in 1 Kbyte blocks (as with df). You can actually read the output by using du -h.

# Tips

+   - If you’re on a system that enforces disk-space quotas (as most ISPs do), you can find out what your quota is and how close you are to reaching it. Just type quota -v at the shell prompt.

+   - You can use du with a path name to check the disk usage in just a single directory or subdirectory (see Code Listing 7.6). du summarizes the usage by subdirectory as it prints the results.

+   - Use du -s, optionally with a specific directory, to just print a summary of the amount of space used.

```
[ejr@hobbes ejr]$ du
2 ./Mail
1 ./nsmail
1 ./netscape/cache/0F
3 ./netscape/cache/1A
22 ./netscape/cache
1 ./netscape/archive
172 ./netscape
1 ./Projects
28 ./wprc
3 ./axhome
5 ./groups
1 ./manipulate/empty
154 ./manipulate
1 ./mail
1 ./unixvqs/ch6
2 ./unixvqs
6 ./dupgroups
255 ./compression/Folder
670 ./compression/temp/BackupFolder
1921 ./compression/temp
670 ./compression/BackupFolder
4657 ./compression
5 ./clean
1 ./elm
15 ./editors
5619 .
[ejr@hobbes ejr]$
```

Code Listing 7.5 The du command reports—exhaustively—about the disk usage in the current directory and in its subdirectories.

```
[ejr@hobbes ejr]$ du /home/ejr/compression
255 /home/ejr/compression/Folder
670 /home/ejr/compression/temp/BackupFolder
1921 /home/ejr/compression/temp
670 /home/ejr/compression/BackupFolder
4657 /home/ejr/compression
[ejr@hobbes ejr]$
```

Code Listing 7.6 Using du with a specific directory name gives you focused results.