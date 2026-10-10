someprogram to run it. Alternatively, you can use a relative path, in which the file is located relative to the current directory. Relative paths don’t begin with a leading slash (/), but take any of several other forms:

+   The name may begin with a double dot (. .), which is the indicator for a given directory’s parent. For instance, in /home/bjolitz, the . . refers to /home. Thus, from that directory, . . / . / opt/bin/someprogram is equivalent to /opt/bin/someprogram.

+   Another form for a relative path is as a subdirectory of the current directory. For instance, from /opt, you might type just bin/someprogram to launch /opt/bin/someprogram.

+   A leading . / indicates that the program file resides in the current directory. Sometimes a current directory (.) entry appears in the path, and if this is the case you can omit the . / characters.

![](bbox=[0.0, 0.4, 0.05, 0.55])

> Using the current directory ( .) entry in the path is risky because it means that FreeBSD executes any program in the current directory as if it were in a standard location for programs, which are normally writable only by root. If you decide to place this entry in the path, do so only at the end of the path, so that the shell searches for common programs in their normal locations before looking in the current directory. This advice is especially important for root because if root has a current directory entry in the path, miscreants could trick root into running unauthentic programs stored in the miscreants’ home directories. Overall, it’s best not to place the current directory entry in any user’s path.

+   A leading tilde (~) indicates a user’s home directory, so ~ /someprogram refers to someprogram in the user’s home directory.

These conventions apply to any file specification, not just those used to launch programs. For instance, if you have to type the name of a file upon which a program operates on the same line as the command, you can use any of these methods. In addition, you can omit the leading . / when referring to a data file in the current directory. You may want to experiment with these techniques using cd (to change to a new directory) and ls (to display the contents of the current directory or the one you specify). If you get lost using cd, type cd alone to return to your home directory, or pwd (short for print working directory) to find out where you are.

Many programs accept options, parameters, or arguments, which are names for additional information fed to a command on the same line as the command itself. For instance, you might pass the name of a file to an editor to have the editor load the file when it loads. Other parameters are program-specific; they change the way the program operates in some way. The upcoming section, “File Manipulation Commands,” includes information on the parameters these commands accept.

If you’re new to UNIX-like OSs, you should be aware that FreeBSD is a case-sensitive OS, meaning that the case of letters in commands and filenames is important. For instance,