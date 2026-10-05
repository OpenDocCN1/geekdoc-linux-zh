
## FOUR MORE UTILITIES

You can use a pipe to send output of a program to the printer:

## FOUR MORE UTILITIES

The echo and date utilities are two of the most frequently used members of the large collection of Linux utilities. The script utility records part of a session in a file, and todos makes a copy of a text file that can be read on either a Windows or a Macintosh machine.

## echo: DISPLAYS TEXT

The echo utility copies the characters you type on the command line after echo to the screen. Figure 5-9 shows some examples. The last example shows what the echo does with an unquoted asterisk (*) on the command line: It expands the asterisk into a list of filenames in the directory.

The echo is a good tool for learning about the shell and other Linux utilities. Some examples on page 257 use echo to illustrate how special characters, such as the asterisk, work. Throughout Chapters 7, 9, and 27, echo explains how shell variables work and how you can send messages from shell scripts to the screen. Refer to the correct page, for more information.

optional You can use echo to create a simple file by redirecting its output to a file:

```
$ echo 'My new file.' > myfile
$ cat myfile
My new file.
```

The greater than (>) sign tells the shell to send the output of echo to the file named myfile instead of the screen. For more information refer to “Redirecting Standard Output” on page 246.

```
$ ls
memo memo.0714 practice
$ echo Hi
Hi
$ echo This is a sentence.
This is a sentence.
$ echo star: *
star: memo memo.0714 practice
$
```

Figure 5-9 echo copies the command line (but not the word echo) to the screen.

## date: DISPLAYS THE TIME AND DATE

The date utility displays the current date and time:

```
$ date
Thu Jan 21 10:24:00 PST 2010
```

The following example shows how you can choose the format and select the contents of the output date:

Refer to the date info page for more information.

## script: RECORDS A SHELL SESSION

The script utility records all or part of a login session, including your input and the system's responses. This utility is useful only from character-based devices, such as a terminal or a terminal emulator. It does capture a session with vim; however, vim uses characters to position the cursor and display different typefaces, such as bold, the output will be difficult to read and may not be useful. When you cat a file that has captured a vim session, the session quickly passes before your eyes.

By default script captures the session in a file named typescript. To specify a different filename, use the script command with a SPACE and the filename. To append to a file, use the -a option after script before the filename; otherwise script overwrites an existing file. Following is a session being recorded by script:

```
$ script
Script started, file is typescript
s whoami
$ ls -l /bin | head -S
total 6632
-rwxr-xr-xr 1 root root 818232 2010-04-10 05:10 bash
-rwxr-xr-xr 1 root root 30200 2010-02-08 02:54 bunzip2
-rwxr-xr-xr 1 root root 1269432 2010-01-22 08:23 busybox
-rwxr-xr-xr 1 root root 30200 2010-02-08 02:54 bzcat
$ exit
Script done, file is typescript
```

Use the exit command to terminate a script session. You can then view the file you created using cat, less, more, or an editor. Following is the file that was created by the preceding script command:

```
$ cat typescript
Script started on Mon Sep 27 20:54:59 2010
$ whoami
s
```

```
$ ls -l /bin | head -5
total 6632
-rw-xr-xr-x 1 root root 818232 2010-04-10 05:10 bash
-rw-xr-xr-x 1 root root 30200 2010-02-08 02:54 bunzip2
-rw-xr-xr-x 1 root root 1269432 2010-01-22 08:23 busybox
-rw-xr-xr-x 1 root root 30200 2010-02-08 02:54 zcat
$
  exit
```

Script done on Mon Sep 27 20:55:29 2010

If you will be editing the file with vim, emacs, or another editor, you can use fromdos
(below) to eliminate from the types file the -M characters that appear at the
ends of lines. Refer to the script man page for information.

## todos: CONVERTS LINUX AND MACINTOSH FILES TO WINDOW FORMAT

If you want to share a text file created on a Linux system with someone on
Windows, use todos.

## COMPRESSING AND ARCHIVING

Large files use a lot of disk space and take longer to transfer over network. If you do not need the file, you may want to save it on CD, DVD.

## bzip2: COMPRESSES A FILE

The bzip2 utility compresses a file by analyzing and recoding it. The new version of the file looks completely different. In fact, the new file contains many nonprinting characters, you cannot view it. The bzip2 utility works practically on files that contain a lot of repeated information, such as text and image data, although most data is already in a compressed format.
