
you first learned DOS, there were only a dozen or so commands that you needed to understand—you could learn the rest as needed. It's the same with Unix. You need learn more only if you want to get more out of Unix.

Also, though you may not realize it, DOS is a kind of subset of Unix. DOS adopted from Unix the idea of a hierarchical file system, as well as the concepts of filters and piping. Moreover, each command that you learned in DOS has a direct parallel in Unix. (See Appendix B, “DOS and Unix Equivalencies.”)

Take a little time to play with each of the commands discussed in this chapter, and you'll be well on your way to becoming a proficient Linux user. If you want to dig deeper, use the man command to get more detailed information on any command. I've listed the most common usage and options for these commands, but there's more if you care to explore.

# 7

# TEXT EDITORS

- THE VI EDITOR 160
- THE EMACS EDITOR 165
- THE PICO EDITOR 171
- THE GNOTEPAD+ EDITOR 175
- THE GEDIT EDITOR 179

For most people, a text editor is the most basic and often-used computer tool. If you want to write a letter, send email, or compose a computer program, you use a text editor to enter your prose and save it in a file.

Although they perform the same basic functions, a text editor and a word processor (such as Word or WordPerfect) are slightly different in nature. In general, a text editor is like a very basic word processing program—it doesn’t offer fancy stuff like fonts, underlining, and boldface. A text editor is useful for entering, updating, and storing text, but you need a word processor to create really sharp-looking documents.

Aside from their differing looks and abilities, text editors and word processors store data in different formats. Text editors store files in plain-text (ASCII) format, which means the files can be read by any other text editor or program, whereas word processors store them in specially coded formats that can be read only by that program. (Actually, most of the popular word processors can read files created by other programs, but you don’t always get the same formatting.) In the DOS/Windows environment, the Edit and Notepad programs are simple text editors, whereas Microsoft Word is a true word processor.

This chapter focuses on three nongraphical Linux text editors (vi, Emacs, and Pico) and two that run under X Windows (Gnotepad+ and gEdit), which can be used to create and modify files. You’ll get an introduction to each one here, and then you can decide which one is best for you.

## THE VI EDITOR

The vi editor comes with every version of Linux or Unix. It’s a terribly unfriendly beast of an editor, but you should know about it because someday you’re likely to find yourself on a system where you have no other choice but to use it. A friend of mine calls vi the Heart of Evil, but that might be just a bit harsh—you decide.

Using vi is similar to using other editors in that you can see your file on the screen (this is not the case with a line editor, for example), move from point to point in the file, and make changes. But that’s where the similarities end. Cryptic commands, a frustrating user interface, and the absence of prompts can all drive you up a wall. Still, if you focus on a few basics, you’ll get the job done.

### COMMAND AND INPUT MODE

The hardest thing to understand about vi is the concept of modes. When using vi, you’re always in either Command or Input mode. Unfortunately, there’s no clue as to which mode is currently active. In Command mode, you can move the cursor, search for characters, and delete existing text. But to enter or edit new text, you have to switch to Input mode.

When you start vi, you’re in Command mode. To enter Input mode, type the letter a (lowercase only) to signal that you want to add text after the cursor position. Press ESC to switch back to Command mode at any time.

Here’s how to create a file from scratch using vi. To start, create a new file named cow.joke by typing

```
vi cow.joke
```

You’ll see a screen that looks like Figure 7-1.

![](img/3137cdda7122042e86dbeafe9840d4ed_192_0.png)

*Figure 7-1: The vi editor screen*
