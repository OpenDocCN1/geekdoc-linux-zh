# 324

# ex

+command | -c command

Begin editing by executing the specified editor command (usually a search or positioning command).

-C Simulate the C command. The C command is like the X command, except that all text read in is assumed to have been encrypted.

-L Set up for editing LISP programs.

-L List the name of all files saved as the result of an editor or system crash.

-R Set the read-only flag to prevent accidental overwriting of the file.

-r file Edit afterlife an editor or system crash. (Recover the version of file that was in the buffer when the crash occurred.) Note that the message file too large to recover with -r option that you see when you load a file indicates that you can successfully edit and save the file. However, if the editing session is lost, you cannot recover the file with the -r option.

-t tag Edit the file containing the tag, and position the editor at its definition.

-V Start up in display-editing state using vi. You can achieve the same effect by simply typing the vi1 command.

-V When commands are read by means of standard input, echo the input to standard error. This verbose option can be useful for processing ex commands within shell scripts.

-wn Set the default window size to n. This option is useful when you are using the editor over a slow-speed line.

-X Simulate the X command, and prompt for an encryption key. This key encrypts and decrypts text using the algorithm of the crypt command. The X command makes an educated guess to determine whether text read is encrypted or not. The temporary buffer file is encrypted also, using a transformed version of the key typed in for -x option.

> Note Although the following options continue to be supported, they have been replaced in the documentation by options that follow the Command Syntax Standard (using incr(1)). The option has been replaced by -si -r option that is not followed by an option- has been replaced by -L, and +command has been replaced by -c command

```
/usr/xpg4/bin/ex
```

If you specify the bo-t tag and -c command, the -t tag is processed first. That is, the file containing tag is selected by -t and then the command is executed.

> Note The Solaris version of ex will be replaced by the POSIX.2-conforming version (using standards(5)) in the future. Scripts that use the ex family of addressing and features should use the /usr/xpg4/bin version of these commands.