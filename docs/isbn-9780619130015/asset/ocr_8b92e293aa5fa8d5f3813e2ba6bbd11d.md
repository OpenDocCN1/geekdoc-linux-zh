4 To exit from superuser mode, type **exit** and then press **Enter**.
5 Test that this file has been correctly copied by typing `man phmenu` and then pressing **Enter**.

In this lesson you learned to check the spelling of a document using the ispell utility. You learned to use the cmp command to check two files that seem similar, to determine any differences between them. Finally, you learned to create your own man page with the groff utility and test it with the man program.

# S U M M A R Y

+   ■ The spell-checking utility, ispell, scans a text document for typing errors.
■ Text formatting in UNIX involves preparing a text file with embedded typesetting commands and then processing the marked-up text file with a computer program that generates commands for the output device.
■ The text containing the embedded typesetting commands is processed (read) by a program like UNIX's nroff and troff utility programs that formats the output.
■ Linux introduced groff, which implements the features of both nroff and troff.
■ Those who have superuser (root) privileges, such as the system administrator, most often create man pages.

# R E V I E W   Q U E S T I O N S

+   1. The groff command is a(n) \_\_\_\_\_\_\_\_\_\_\_.
   a. text formatting utility
   b. man page utility
   c. search text utility
   d. editor
2. True or false: The ispell utility only displays misspelled words. It does not allow you to change the misspelled words.
3. The embedded commands used by groff to format a text file are placed in the \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.
   a. command line
   b. file itself
   c. same directory as the text file, in a special command file
   d. man1 directory