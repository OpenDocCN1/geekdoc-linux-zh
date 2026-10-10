
## Review Questions

1. You type a command into **bash** and pass a long filename to it, but after you enter the command, you receive a `File not found` error message because of a typo in the filename. How might you proceed?
   - A. Retype the command, and be sure you type the filename correctly, letter by letter.
   - B. Retype the command, but press the `Tab` key after typing a few letters of the long filename to ensure that the filename is entered correctly.
   - C. Press the `Up arrow` key, and use **bash**’s editing features to correct the typo.
   - D. Any of the above.

2. Which of the following commands is implemented as an internal command in **bash**?
   - A. `cat`
   - B. `echo`
   - C. `tee`
   - D. `sed`

3. You type `echo $PROC`, and the computer replies `Go away`. What does this mean?
   - A. No currently running processes are associated with your shell, so you may log out without terminating them.
   - B. The remote computer `PROC` isn’t accepting connections; you should contact its administrator to correct the problem.
   - C. Your computer is handling too many processes; you must kill some of them to regain control of the computer.
   - D. You, one of your configuration files, or a program you’ve run has set the `$PROC` environment variable to `Go away`.

4. What does the `pwd` command accomplish?
   - A. It prints the name of the working directory.
   - B. It changes the current working directory.
   - C. It prints wide displays on narrow paper.
   - D. It parses Web page URLs for display.

5. In an `xterm` window launched from your window manager, you type `exec gedit`. What will happen when you exit from the `gedit` program?
   - A. Your shell will be a `root` shell.
   - B. The `gedit` program will terminate, but nothing else unusual will happen.
   - C. Your X session will terminate.
   - D. The `xterm` window will close.

6. What is the surest way to run a program (say, myprog) that's located in the current working directory?
   - A. Type `./` followed by the program name: `./myprog`.
   - B. Type the program name alone: `myprog`.
   - C. Type `run` followed by the program name: `run myprog`.
   - D. Type `/`, followed by the program name: `/myprog`.

7. How does `man` display information by default on most Linux systems?
   - A. Using a custom X-based application
   - B. Using the Firefox Web browser
   - C. Using the `less` pager
   - D. Using the Vi editor

8. You want to store the standard output of the `ifconfig` command in a text file (`file.txt`) for future reference, and you want to wipe out any existing data in the file. How can you do so?
   - A. `ifconfig < file.txt`
   - B. `ifconfig >> file.txt`
   - C. `ifconfig > file.txt`
   - D. `ifconfig | file.txt`

9. What is the effect of the following command?
   - `$ myprog &> input.txt`
   - A. Standard error to `myprog` is taken from `input.txt`.
   - B. Standard input to `myprog` is taken from `input.txt`.
   - C. Standard output and standard error from `myprog` are written to `input.txt`.
   - D. All of the above.

10. How many commands can you pipe together at once?
    - A. 2
    - B. 3
    - C. 4
    - D. An arbitrary number

11. You want to run an interactive script, `gabby`, which produces a lot of output in response to the user's inputs. To facilitate future study of this script, you want to copy its output to a file. How might you do this?
    - A. `gabby > gabby-out.txt`
    - B. `gabby | tee gabby-out.txt`
    - C. `gabby < gabby-out.txt`
    - D. `gabby &> gabby-out.txt`

12. A text-mode program, `verbose`, prints a lot of spurious "error" messages to standard error. How might you get rid of those messages while still interacting with the program?
    - A. `verbose | quiet`
    - B. `verbose &> /dev/null`
    - C. `verbose 2> /dev/null`
    - D. `verbose > junk.txt`

13. How do the `>` and `>>` redirection operators differ?
    - A. The `>` operator creates a new file or overwrites an existing one; the `>>` operator creates a new file or appends to an existing one.
    - B. The `>` operator creates a new file or overwrites an existing one; the `>>` operator appends to an existing file or issues an error message if the specified file doesn’t exist.
    - C. The `>` operator redirects standard output; the `>>` operator redirects standard error.
    - D. The `>` operator redirects standard output; the `>>` operator redirects standard input.

14. What program would you use to display the end of a configuration file?
    - A. `uniq`
    - B. `cut`
    - C. `tail`
    - D. `wc`

15. What is the effect of the following command?
    - `$ pr report.txt | lpr`
    - A. The file `report.txt` is formatted for printing and sent to the `lpr` program.
    - B. The files `report.txt` and `lpr` are combined together into one file and sent to standard output.
    - C. Tabs are converted to spaces in `report.txt`, and the result is saved in `lpr`.
    - D. None of the above.

16. Which of the following commands will number the lines in `aleph.txt`? (Select all that apply.)
    - A. `fmt aleph.txt`
    - B. `n1 aleph.txt`
    - C. `cat -b aleph.txt`
    - D. `cat -n aleph.txt`

17. Which of the following commands will change all occurrences of `dog` in the file `animals.txt` to `mutt` in the screen display?
    - A. `sed -s 'dog' 'mutt' animals.txt`
    - B. `grep -s 'dog||mutt' animals.txt`
    - C. `sed 's/dog/mutt/g' animals.txt`
    - D. `cat animals.txt | grep -c 'dog' 'mutt'`

18. You've received an ASCII text file (`longlines.txt`) that uses no carriage returns within paragraphs but two carriage returns between paragraphs. The result is that your preferred text editor displays each paragraph as a very long line. How can you reformat this file so that you can more easily edit it (or a copy)?
    - A. `sed 's/Ctrl-M NL/  ' longlines.txt`
    - B. `fmt longlines.txt > longlines2.txt`
    - C. `cat longlines.txt > longlines2.txt`
    - D. `pr longlines.txt > longlines2.txt`

19. Which of the following commands will print lines from the file `world.txt` that contain matches to `changes` and `changed`?
    - A. `grep change[ds] world.txt`
    - B. `sed change[d-s] world.txt`
    - C. `od "change'd|s" world.txt`
    - D. `cat world.txt changes changed`

20. Which of the following regular expressions will match the strings `dig` and `dug` but not `dog`?
    - A. `d.g`
    - B. `d[iu]g`
    - C. `d[i-u]g`
    - D. `di*g`

## Answers to Review Questions

1. D. Any of these approaches will work, or at least *might* work. (You might err when performing any of them.) Option B or C is likely to be the most efficient approach; with a long filename to *type*, option *A* is likely to be tedious.

2. B. The `echo` command is implemented internally to `bash`, although an external version is also available on most systems. The `cat`, `tee`, and `sed` commands are not implemented internally to `bash`, although they can be called from `bash` as external commands.

3. D. The `echo` command echoes what follows to standard output, and `$PROC` is an environment variable. Thus, `echo $PROC` displays the value of the `$PROC` environment variable, meaning that it must have been set to the specified value by you, one of your configuration files, or a program you’ve run. Although many environment variables are set to particular values to convey information, `$PROC` isn’t a standard environment variable that might be associated with information described in options *A*, *B*, or *C*.

4. A. The `pwd` command prints (to standard output) the name of the current working directory. The remaining options are simply incorrect, although option B describes the `cd` command and various tools can be used to reformat wide text for display or printing in fewer columns, as in option C.

5. D. The `exec` command causes the rest of the command to replace the current shell. Thus, when you exit from `gedit` in this scenario, the result will be the same as if you’d terminated the shell, namely, the `xterm` window will close. The `exec` command doesn’t raise the execution privilege, so option *A* is incorrect. (The `su` and `sudo` commands can raise execution privilege, though.) Because the `xterm` window closes, option *B* is incorrect. X won’t ordinarily terminate when a single `xterm` does, and definitely not if that `xterm` was launched from a window manager, so option *C* is incorrect.

6. A. The dot (`.`) character refers to the current working directory, and the slash (`/`) is a directory separator. Thus, preceding a program name by `./` unambiguously identifies the intention to run the program that’s stored in the current *directory*. Option B will run the first instance of the program that’s found on the current path. Because paths often omit the current directory for security reasons, this option is likely to fail. The `run` command isn’t a standard Linux command, so option *C* is unlikely to do anything, much less what the question specifies. Option D would be correct except that it reverses the order of the two characters. The effect is to attempt to run the `.myprog` file in the root (`/`) directory. This file probably doesn’t exist, and even if it did, it’s not the file the question specifies should be run.

7. C. By default, `man` uses the `less` pager to display information on most Linux systems. Although an X-based version of `man` does exist (`xman`), the basic `man` doesn’t use a custom X-based application, nor does it use Firefox or the VI editor.
