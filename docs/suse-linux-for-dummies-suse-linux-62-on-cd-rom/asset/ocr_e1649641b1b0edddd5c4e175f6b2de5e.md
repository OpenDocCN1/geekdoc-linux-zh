# Conventions without Shiners

You'll be seeing a list of commands, so you might find it helpful to review the syntax of Linux commands:

+   Text inside angle brackets > must be replaced with appropriate text.

+   Text inside braces {} indicates that you must choose one of the values that are inside the braces separated by the | sign.

+   Text not surrounded by {}, {}, or > must be typed exactly as shown.

+   Text inside brackets [] is optional.

+   An ellipsis (...) means so and on to repeat the preceding command line as needed.

Type this command:

```
ls -la
```

The files you see are only those in your working directory. If you want to specify a file that isn't in your working directory, you must name the directory that contains the file, as well as the name of the file. For example, the following command lists the passwd file in the /etc directory:

```
ls -la /etc/passwd
```

# Every directory has a parent and lots of relatives

If the file you want to read is in a subdirectory of the one you are in, you can reach the file by typing a relative filename. Relative filenames specify the location of files relative to where you are.

In addition to what we told you about specifying directory paths, you need to know about these three additional rules:

+   One dot (.) always stands for the current directory.

+   Two dots (..) specify the parent directory of the directory you are currently in.

+   All directory paths that include (.) or (..) are relative directory paths.

You can see these files using the -a option of the ls(-1) command. Without the -a option, the ls(1) command does not bother to list the . or .. files, nor does it list any filename beginning with a period.