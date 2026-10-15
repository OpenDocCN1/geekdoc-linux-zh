
## Importing Files into vi

You can also merge multiple files in vi by reading additional files into the current one, as shown in Figure 4.13. Basically, all this means is that you insert one file into the file you're currently editing.

### To import files in vi:

1. `vi hairyspider`

   At the shell prompt, type `vi` followed by the filename to start vi with, in this case, the `hairyspider` file.

2. `Esc :r filename`

   At the point in the file where you want to import text, press `Esc`, then type `:r` and the filename you want to read into the file.

### Tip

vi also lets you read the output of commands into the file. For example, if you want to read the list of files in a specific directory into the file, use `Esc :r !ls` in command mode.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_96_0.png)

## Searching and Replacing in vi

One of vi’s better features (and advantages over pico) is that it allows you to search and replace throughout entire files. As shown in the next sections, you can just find a specific string of text (a regular expression, in Unix lingo; see Figure 4.14), or you can find the text and replace it with other text, as in Figure 4.15.

### To find a string of text in vi:

1. `vi hairyspider`

   For starters, access vi and a specific file.

2. `Esc` `/spider`

   Enter command mode, then type `/` followed by the text you’re looking for. Here, we’re looking for “spider,” but you may be looking for “the fly” or “wiggled and jiggled and tickled inside her.” Or whatever.

3. `Enter`

   Press this to find the first occurrence of the term. Press `N` to find the next one.

### To search and replace in vi:

1. `vi hairyspider`

   For starters, access vi and a specific file.

2. `Esc:%s/swallowed the fly/swallowed a spider to catch the fly/`

   Enter `Esc:%s/` plus the text to find, followed by the replacement text, as in Figure 4.15. Here, we replace “swallowed a fly” with “swallowed a spider to catch the fly,” but perhaps you might forego the spider and simply go for some antacid.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_97_0.png)

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_97_1.png)

## ✓ Tips

- A great use for the search-and-replace feature is if you end up with DOS text files in your Unix account (through uploading a text file from a DOS or Windows machine as a binary file, most likely). If you view DOS files through a Unix shell, all the lines within the file will end with `^M`. But if you try to type `^M` when you're doing a search and replace, the `^M` won't show up. What to do? Press `Ctrl V`, then `Ctrl M`. Just search and replace with `:%s/ Ctrl V Ctrl M Ctrl M /g`. The `Ctrl V` command "escapes" the following character, so you can type it without actually doing what the command would otherwise do. If you don't escape the `Ctrl M`, vi thinks you just pressed `Enter` and tries to execute the unfinished command.

- See the section on grep in Chapter 6 for information about searching with regular expressions.

- Add a `g` at the end of the command to make it apply to all occurrences in the file. Otherwise, it applies only to the first occurrence on each line.

## Exiting vi

Whew! Time to exit vi (Figure 4.16).

### To exit vi:

`Esc :q`

Enter command mode with `Esc`, then type `:q` to quit vi. If you haven't saved your latest changes, vi will not quit and will tell you to use `!` to override. To quit without saving your changes, use `:q!`, as shown in Figure 4.16.

### Tips

- If you don't really want to quit but want to edit a different file instead, type `:e filename` to open a new file to edit.
- We recommend that you take a few minutes and try out some of the commands that you'll use throughout your vi experience. If you don't think you'll be needing this range of commands, consider using pico rather than vi.
- It takes some practice to get accustomed to vi, but the time spent is well worth it. With patience and practice, you'll quickly become proficient in using vi. Take your time, take deep breaths, and plow ahead.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_99_0.png)

Figure 4.16 Use `Esc :q!` to quit vi without saving changes.
