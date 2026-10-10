+   15. Output the text string hello on the screen of terminal tty1 (provided that tty1 has not set msg n).

# Chapter 8

+   1. $ find / -name 'mis*' -type f<Enter>

+   2. List all processes that begin with the /sbin string in their respective command paths and that belong to the root user. The -w option is a bit of a red herring (or, if you are an Alfred Hitchcock movie fan, a “McGuffin”). The -w option simply ensures that searches are performed on the whole word so that usernames or processes that contain the respective strings, but which form only part of longer strings, are not included in the output.

+   3. A recursive long listing is carried out from the /home/username directory downward through the file system. We will be looking for listings of lines that end in um or isc or that contain snc. (We are using egrep because we need to do a sort of OR grep. Then, we take those long-listed file entries (as lines) and pipe them to the sort command. The sort command sorts the lines in reverse order based on the eighth field (that is, on the filenames themselves). Some but not all results are presented. The display begins with the second line, and only seven lines are displayed. As you can surmise, this complex command might require you to continue the command from the first command line, with the primary PS1 prompt, to the second command line with its secondary PS2 prompt.

# Chapter 9

+   1. False. Unfortunately, find travels only recursively down through a file system structure.

+   2. find itself. This time, the quoting metacharacters are used to keep the interpretation away from the shell.

+   3. file is the command that reports to you on the type of files you choose to examine.

+   4. False. Everything is true except that the extension is .gz, not just .z.