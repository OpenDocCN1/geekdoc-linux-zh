# Chapter 4: Simple Variables 199

Many people like to put $HISTCMD in their prompt string so they will know what command number to use with the shell's r built-in command. The r command reruns a previously entered command, using either the command number (what you see if you put the value of HISTCMD in your prompt string) or a piece of the previous command line, such as the initial few letters. See Appendix B,"Summary of Built-In Commands," for a summary of the r command and the history command that is often used in conjunction with it during interactive sessions.

Instead of the current directory, put the command line number inside the square brackets of your command prompt.

+   - What happens if you press Enter at the beginning of a line, compared with entering a command?

# 4.3.3 QUOTE SINGLE CHARACTERS

There is another type of quoting you can use that works the same way as single quotes but applies to single characters. The backslash (\) character tells the shell that the next character is to be treated literally as that character, not as a character that might otherwise have significance to the shell as it analyzes the command line.

This type of quoting is sometimes called a literal escape or an escape quote.

> The backslash as a quoting character has nothing to do with the ASCII <Esc> code, even though the word escape is used for both, don't confuse the two.

# FOR EXAMPLE

You could use the following command to set PSI the same way you set it in the previous exercise: