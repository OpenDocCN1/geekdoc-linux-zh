the application. Instead of the wildcard characters, for instance, the program would receive a space-delimited list of all files matching the wildcard construct. The user may restrict this capability if the wildcard characters are intended to be interpreted by the program rather than the shell. There are three wildcard characters frequently used in Linux, each interpreted differently by the Bash shell: the asterisk, the question mark, and the bracket pair.

The asterisk is often called the “splat”; the string b*.bmp might be pronounced as “b–splat–dot–bmp.” Its purpose is to replace a string of any number of characters in sequence. Thus b*.bmp matches with any file whose name begins with b and has the .bmp extension. The files blue.bmp, barney.bmp, bermuda.bmp, and before_you_go_away.bmp would all match.

The string *.* matches all files that contain a period; be certain that you really mean to act on all files in the directory when you use this string. The string .* matches any dot file.

Many a user has deleted important files by specifying an incorrect wildcard string as an argument to the rm command. The “joke” that is often played is trying to get the new guy to run rm –rf * from the root directory. This is a forced removal of all files and directories. It’s ugly if you have no backup.

The question mark represents any one character. The string file_? would match all of the following: file_1, file_2, file_A, or file_b. The string file.??? would match any file named file that has a three-character extension.

The bracket pair is used to define a list or range of characters to be matched. The string file[0–9] would match file0, file1, file9. The string [a–zA–Z] would match any single alphabetical character. The string [a–zA–Z0–9] would match any alpha or numeric character.

# ## Quoting

As you’ve seen, shell commands assign special meanings to ordinary alphanumeric characters, so when these characters are used within strings literally, there needs to be some way to prevent the shell from interpreting the characters. In the Bash shell, quoting is the basic technique for this. There are three quoting mechanisms: the escape character, single quotes, and double quotes:

+   - The backslash (\) is the Bash escape character. It causes the next character to be taken literally.

+   - Single quotes preserve the literal value of each character within the quotes. A single quote may not occur between single quotes, since the enclosed quote would be interpreted as the closing single quote.

+   - Double quotes protect the literal value of all characters contained within, except for the dollar sign ($), the tick mark (`’`), the double quote (`"`), and the backslash (`\`). If a quoted string contains an environment variable that is to be expanded, double quotes allow this. Single quotes prevent the expansion.

# ## The Tilde

The tilde can save you several keystrokes every day. If a pathname/file combination begins with a tilde, everything preceding the first / is treated as a possible login name. In the case of ~/user/some_files, the ~/user would be replaced by the home directory of user. In most cases, this would be expanded to /home/user/some_files. If the resulting login name is a null string, as in ~/myfile, the tilde is replaced by the username of the user who executed the command.

If the tilde is followed by a plus sign, the ~+ is replaced by the present working directory. If the plus