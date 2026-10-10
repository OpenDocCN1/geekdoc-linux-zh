# Basic Commands

We have already discussed how many parameters `less` is capable of taking, but they can be distilled down to three that are very useful: `-M`, `-N`, and `+`. Adding `-M` (this is different from `-m`) enables verbose prompting in `less`. Instead of just printing a colon and a flashing cursor, `less` prints the filename, the line numbers being shown, the total number of lines, and the percentage of how far you are through the file. Adding `-N` (again, this is different from `-n`) enables line numbering.

The last option, `+`, enables you to pass a command to `less` for it to execute as it starts. To use this, you first need to know the commands available to you in `less`, which means we need to move onto the second category of `less` input: what you type while `less` is running.

The basic navigation keys are the up, down, left, and right cursors; Home and End (for navigating to the start and end of a file); and Page Up and Page Down. Beyond that, the most common command is `/`, which initiates a text search. You type what you want to search for and press Enter to have `less` find the first match and highlight all subsequent matches. Type `/` again and press Enter to have `less` jump to the next match. The inverse of that is `?`, which searches backward for text. Type `?`, enter a search string, and press Enter to go to the first previous match of that string, or just use `?` and press Enter to go to the next match preceding the current position. You can use `/` and `?` interchangeably for searching for something with `/` and then using `?` to go backward in the same search. Searching with `/` and `?` is commonly done with the `+` command-line parameter from earlier, which passes `less` a command for execution after the file has loaded. For example, you can tell `less` to load a file and place the cursor at the first match for the search `hello`, like this:

```
$ less +/hello myfile.txt
```

Or, you can tell it to place the cursor at the last match for the search `hello`:

```
$ less +?hello myfile.txt
```

Beyond the cursor keys, the controls primarily involve typing a number and then pressing a key. For example, to go to line 50, type `50g`; or to go to the 75% point of the file, type `75p`. You can also place invisible mark points through the file by pressing `m` and then typing a single letter. Later, while in the same `less` session, you can press `’` (a single quote) and then type the letter, and you will move back to the same position. You can set up to 52 marks, named `a-z` and `A-Z`.

One clever feature of `less` is that you can, at any time, press `v` to have your file opened inside your text editor. This defaults to Vim, but you can change that by setting the EDITOR environment variable to something else.

If you have made it this far, you can already use `less` better than most users. You can, at this point, justifiably skip to the next section and consider yourself proficient with `less`. However, if you want to be a `less` guru, there are two more things to learn: how to view multiple files simultaneously and how to run shell commands.