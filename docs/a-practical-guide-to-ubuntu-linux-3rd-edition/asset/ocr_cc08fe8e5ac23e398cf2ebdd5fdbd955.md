# date: DISPLAYS THE TIME AND DATE

The date utility displays the current date and time:

```
$ date
Thu Jan 21 10:24:00 PST 2010
```

The following example shows how you can choose the format and select the contents of the output of date:

```
$ date "+%A %B %d"
Thursday January 21
```

Refer to the date info page for more information.

# script: RECORDS A SHELL SESSION

The script utility records all or part of a login session, including your input and the system's responses. This utility is useful only from character-based devices, such as a terminal or a terminal emulator. It does capture a session with vim; however, because vim uses control characters to position the cursor and display different typefaces, such as bold, the output will be difficult to read and may not be useful. When you cat a file that has captured a vim session, the session quickly passes before your eyes.

By default script captures the session in a file named typescript. To specify a different filename, follow the script command with a SPACE and the filename. To append to a file, use the -a option after script but before the filename; otherwise script overwrites an existing file. Following is a session being recorded by script:

```
$ script
Script started, file is typescript
$ whoami
sam
$ ls -l /bin | head -5
total 6632
-rwxr-xr-x 1 root root 818232 2010-04-10 05:10 bash
-rwxr-xr-x 1 root root 30200 2010-02-08 02:54 bunzip2
-rwxr-xr-x 1 root root 1269432 2010-01-22 08:23 busybox
-rwxr-xr-x 1 root root 30200 2010-02-08 02:54 bzcat
$ exit
exit
Script done, file is typescript
```

Use the exit command to terminate a script session. You can then view the file you created using cat, less, more, or an editor. Following is the file that was created by the preceding script command:

```
$ cat typescript
Script started on Mon Sep 27 20:54:59 2010
$ whoami
sam
```