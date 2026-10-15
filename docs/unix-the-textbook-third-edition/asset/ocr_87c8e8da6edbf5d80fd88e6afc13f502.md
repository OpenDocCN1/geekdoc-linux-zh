Step 7: Type 1G. This action puts the cursor on the first character of the first line in the buffer.

Step 8: Hold down the <Shift> and ; keys at the same time. Doing so places a : in the status line at the bottom of the vi screen display, allowing you to type a command.

Step 9: Type s/everyone/students/ and then press <Enter>. The word everyone at the end of the first line is replaced with the word students.

Step 10: Use the arrow keys to position the cursor on the first character of the second line.

Step 11: Type :s/everyone/computer scientists/ and then press <Enter>.

Step 12: Repeat Steps 8–10 on the third through eighth lines of the buffer, substituting the words engineers, system administrators, web servers, scientists, networking, and mathematicians for the word everyone on each of those six lines.

Step 13: Type :1,$s/Windows/UNIX/g and then press <Enter>. You have globally replaced the word Windows on all eight lines of the file with the word UNIX. Correct?

Step 14: Type :wq. You have now saved the changes and exited from vi.

# 3.2.6 vim and gvim

Vim and gvim are two examples among many of enhanced, “improved” versions of vi. The following subsections illustrate some of the advantages of using vim and gvim over the traditional vi editor.

# 3.2.6.1 Vim Enhancements

The following capabilities of vim that enhance vi functionality, particularly the first one shown, are suggestions that you can use to expedite your editing tasks with vim and gvim over and above the capabilities of vi:

+   * vimrc

If you want to enable any of the improved facilities of vim and gvim, you should create a ~/.vimrc file. Even if this file is empty, it will enable the facilities that we illustrate in this section!

+   * Help

In vim Last Line mode, type help or press the F1> function key.

Vim opens a help buffer that gives you extensive help on its facilities. In Last Line mode, when in the help buffer, type q to exit help.

+   * Multiple Windows