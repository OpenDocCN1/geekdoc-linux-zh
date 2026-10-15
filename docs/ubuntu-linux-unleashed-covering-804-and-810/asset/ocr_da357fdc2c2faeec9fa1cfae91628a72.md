the source file. The `--color` parameter tells grep to color the search terms in the output, which helps them stand out when among all the other text on the line. You choose which color you want using the `GREP_COLOR` environment variable: export `GREP_COLOR=36` gives you cyan, and export `GREP_COLOR=32` gives you lime green.

This next example uses these two parameters to number and color all matches to the previous command:

```
grep -in --color [cms]at myfile.txt
```

Later you will see how important grep is for piping with other commands.

# Paging Through Output with less

The less command enables you to view large amounts of text in a more convenient way than the cat command. For example, your /etc/passwd file is probably more than a screen long, so if you run cat /etc/passwd, you are not able to see what the lines at the top were. Using less /etc/passwd enables you to use the cursor keys to scroll up and down the output freely. Type q to quit and return to the shell.

On the surface, less sounds like a very easy command; however, it has the infamy of being one of the few Linux commands that have a parameter for every letter of the alphabet. That is, -a does something, -b does something else, -c, -d, -e, -f, -g, -h, -i, -j, -k, -l, and so on—they all do things, with some letters even differentiating between upper- and lowercase. Furthermore, it is only the parameter used to invoke less. After you are viewing your text, even more commands are available to you. Make no mistake—less is a complex beast to master.

Input to less can be divided into two categories: what you type before running less and what you type while running it. The former category is easy, so we shall start there.

We have already discussed how many parameters less is capable of taking, but they can be distilled down to three that are very useful: `-M`, `-N`, and `+`. Adding `-M` (this is different from `-m!`) enables verbose prompting in less. Rather than just printing a colon and a flashing cursor, less prints the filename, the line numbers being shown, the total number of lines, and the percentage of how far you are through the file. Adding `-N` (again, this is different from `-n`) enables line numbering.

The last option, `+`, allows you to pass a command to less for it to execute as it starts. To use this, you first need to know the commands available to you in less, which means we need to move onto the second category of less input: what you type while less is running.

The basic navigation keys are the up, down, left, and right cursors; Home and End (for navigating to the start and end of a file); and Page Up and Page Down. Beyond that, the most common command is `/`, which initiates a text search. You type what you want to search for and press Enter to have less find the first match and highlight all subsequent matches. Type `/` again and press Enter to have less jump to the next match. The inverse of that is `?`, which searches backward for text. Type `?`, enter a search string, and press Enter to go to the first previous match of that string, or just use `?` and press Enter to go to the next match preceding the current position. You can use `/` and `?` interchangeably by searching for something with `/` and then using `?` to go backward in the same search.