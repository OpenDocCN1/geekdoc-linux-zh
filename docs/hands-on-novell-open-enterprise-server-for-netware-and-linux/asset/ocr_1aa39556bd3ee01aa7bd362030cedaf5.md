A user logs in. The syntax of the CONTEXT command includes the typeful distinguished name of the container that will become the default context. To set the default container to the IT OU, for example, enter this command:

```
CONTEXT .OU=IT.O=UAS
```

Being able to change the context is important when using Directory Map objects and volume names in login script MAP commands. If the context isn't changed to the correct container, the Directory Map object might not be found or the wrong volume could be used. For example, Kellie often needs to log in from other users' computers to test software. To use her distinguished name instead of selecting the context in the Novell Login window each time she logs in, she included the CONTEXT .OU=IT.O=UAS command in the IT container login script.

# The WRITE Command

The WRITE command is used to display simple messages on users' computers. Messages can also contain identifier variables and special control strings, as shown:

```
WRITE "text control string VARIABLE"
```

Common login script variables used with WRITE include %GREETING_TIME and %LOGIN_NAME (described in Tables 4-5 and 4-6). For example, the following WRITE statement displays a greeting message with the login time and user's full name:

```
WRITE "Good %GREETING_TIME, %LOGIN_NAME"
```

Follow important messages with the PAUSE command to make sure users have time to read the message. In Activity 9-9, you learn how to modify your existing login script to use the WRITE command.

# The DISPLAY and FDISPLAY Commands

The DISPLAY and FDISPLAY (for "filtered display") commands are used to show the contents of an ASCII text file on-screen when the login script runs. This is the syntax for both commands:

```
DISPLAY (or FDISPLAY) directory_path filename
```

If filename is in the current directory, or if a search drive has been established to the directory containing filename, the directory path isn't needed. However, in the following example, even though a search drive has been created for SYS:Public, the Welcome.msg file is in the Message subdirectory. You need to use the directory_path parameter to make sure the message file is found:

```
MAP INS S1:=SYS:Public
FDISPLAY SYS:Public\Message\Welcome.msg
PAUSE
```

![](bbox=[0.115, 0.705, 0.19, 0.77])

An error message is displayed if the file specified in the DISPLAY command doesn't exist.

You should follow DISPLAY or FDISPLAY with a PAUSE command to give users time to read the message. The difference between DISPLAY and FDISPLAY is that FDISPLAY "filters" and formats the specified file's contents so that only ASCII text is displayed. For example, FDISPLAY doesn't display tab characters, but converts them into spaces to make the output more readable. The DISPLAY command displays the exact characters in the file, including "garbage" characters such as printer or word-processing edit codes. Using FDISPLAY is usually preferable; however, if you use a word processing file, be sure to save it in ASCII text format, or not even FDISPLAY can read it.