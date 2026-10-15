
## Preview of the Next Hour

The next hour expands your knowledge of the vi editor. It introduces you to the sophisticated search and replace capability, explores the useful colon commands, and details the command-line options you’ll want to know.

## Hour 11: Advanced vi Tricks, Tools, and Techniques

### Goals for This Hour

In this hour, you will learn

- How to search within a file
- How to search and replace
- How to have vi start correctly
- The key colon commands in vi
- The change and replace commands
- How to use the `:!` command to access Unix commands

In the preceding hour, you learned what probably seems like a ton of vi commands to enable you to easily move about in files, insert text, delete other text, and move from file to file without leaving the program. This hour expands your expertise by showing you some more powerful vi commands. Before you begin this hour, I strongly recommend that you use vi to work with a few files to ensure that you’re comfortable with the different modes of the program.

This might seem like a small list, but there’s a lot packed into this hour. I’ll be totally honest: You can do fine in vi without ever reading this particular lesson. You already know how to move around, how to insert and delete text, and how to save your changes or quit the program without saving! But vi is like any other complex topic: The more you’re willing to study and learn, the more the program will bow to your needs. This means you can accomplish a wider variety of daily tasks more efficiently.

### Advanced Editing with vi

The preceding hour focused on the basics of inserting and deleting text and moving around within a file. This hour adds a critical capability: searching and replacing text within a file.

### Task 11.1: Searching Within a File

With the addition of two more capabilities, you’ll be ready to face down any vi expert, demonstrating your skill and knowledge of the editor, and, much more importantly, you will be able to really fly through files, moving immediately to the information you desire for further edits.

The same pattern.

You can move easily to any specific line in a file by using the G, or go-to-line, command. If you type a number before you type G, the cursor will move to that line in the file. If you type G without a line number, the cursor will zip you to the last line of the file (by default).

1. Start vi again with the big.output file with the command `vi big.output`:

```text
leungtc ttyrV Dec  1 18:27 (magenta)
tuyinhwa ttyX Dec  3 22:38 (expert)
hollenst ttyrZ Dec  3 22:14 (dov)
brandt ttyrb Nov 28 23:03 (age)
holmes ttyrj Dec  3 21:59 (age)
yuxi ttyrn Dec  1 14:19 (pc)
frodo ttyro Dec  3 22:01 (mentor)
labeck ttyrt Dec  3 22:02 (dov)
chenlx2 ttyru Dec  3 21:53 (mentor)
leungtc ttyso Nov 28 15:11 (gold)
chinese ttys2 Dec  3 22:53 (excalibur)
cdemmert ttys5 Dec  3 23:00 (mentor)
yuenca ttys6 Dec  3 23:00 (mentor)
janitor ttys7 Dec  3 18:18 (age)
mathisbp ttys8 Dec  3 23:17 (dov)
janitor ttys9 Dec  3 18:18 (age)
cs541 ttysC Dec  2 15:16 (solaria)
yansong ttysL Dec  1 14:44 (math)
mdps ttysO Nov 30 19:39 (localhost)
md ttysU Dec  2 08:45 (muller)
jac ttysa Dec  3 18:18 (localhost)
eichsted ttysb Dec  3 23:21 (pcl)
sweett ttysc Dec  3 22:40 (dov)
"big.output" 40 lines, 1659 characters
```

Remember that I used `:q!` to quit earlier, so my changes were not retained. (I know you’re paying super-close attention to these examples!)

To move to the last line of the file, I type G once, and I see this:

```text
cdemmert ttysk Dec  3 22:37 (xsun)
jrlee ttysn Dec  3 22:53 (mac1)
fitzgejs ttyso Dec  3 23:18 (dov)
doerrhb ttysp Dec  3 23:20 (dov)
cdemmert ttysq Dec  3 23:00 (xsun)
frazierw ttysr Dec  3 23:01 (dov)
buckeye ttyss Dec  3 23:20 (mac2)
mtaylor ttyst Dec  3 23:22 (dov)
look ttysu Dec  3 23:12 (age)
janitor ttysw Dec  3 18:29 (age)
ajones ttysx Dec  3 23:23 (rassilon)
~
~
~
~
~
~
~
~
```
