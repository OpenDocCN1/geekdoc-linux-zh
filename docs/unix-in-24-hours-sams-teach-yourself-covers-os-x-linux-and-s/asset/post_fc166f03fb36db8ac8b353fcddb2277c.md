
2. The `-f` flag in `awk` lets you change field delimiters. How would you use `awk` to extract all the home directories out of the `/etc/passwd` file?

3. `ROT13` is useful, but `ROT7` could be even better. How would you write aliases for both encoding and decoding a `ROT7` system?

4. The output of `ls -l` has the file permission shown as a character sequence: `rwx`, `r-x`, and so on. Can you come up with a combination of `cut` and `grep` to identify whether you have any files that have only `write` or `execute` permission?

5. Using `tr`’s class identifiers and its `-d` flag (read the man page to find out what it does), how would you remove all punctuation characters from your input stream?

## Preview of the Next Hour

In the next hour you’ll learn about the powerful and phenomenally useful `vi` editor, which will doubtless seem weird and puzzling when you get started. But `vi` is a mainstay in any good Unix user’s repertoire and can make editing quite a bit faster than even the best graphically based application.

## Hour 10. An Introduction to the vi Editor

### Goals for This Hour

In this hour, you will learn

- How to start and quit vi
- Simple cursor motion in vi
- How to move by words and pages
- How to insert text into a file
- How to delete text

The next few hours focus on full-screen editing tools for Unix. First you’ll learn how to use vi to create and modify files. This hour covers the basics, including how to move around in a file and how to insert and delete characters, words, and lines. The next hour shows how to search for specific patterns in the text and how to replace them with other information, as desired. In Hour 12, “An Overview of the emacs Editor,” you’ll learn to use an alternative Unix editor called emacs. As you work with emacs and vi, you’re likely to develop a preference for one or the other.

In some ways, an editor is like another operating system living within Unix; we’ll need two hours just to cover the basics of vi. If you’re used to Windows or Macintosh editors, you’ll be unhappy to find that vi doesn’t know anything about your mouse. After you spend some time working with vi, however, I promise it will grow on you because it’s so super-efficient to work without ever lifting your hands off the keyboard to use the mouse! By the end of this hour, you will be able to create and modify files on your Unix system to your heart’s content.

### Tip

I pronounce the editors as “vee-ee” and “e-max.”

### Editing the Unix Way

You’ve learned about how to manipulate your files and even peek inside them from the command line, and now it’s time to learn the key Unix tool for creating and editing files: vi.

### Task 10.1: Starting and Quitting vi

You might have noticed that many Unix commands covered so far have one characteristic in common: They all do their work, display their results, and quit. Among the few exceptions is more, in which you work within the specific program environment until you have viewed the entire contents of the file being shown or until you quit. The vi editor is another program in this small category that you move in and use until you explicitly tell the program to quit.

### Note

Where did vi get its name? It’s not quite as interesting as some of the earlier, more colorful commands. The vi command is so named because it’s the visual interface to the ex editor. It was written by Bill Joy while he was at the University of California at Berkeley.

Before you start vi for the first time, you must learn about two aspects of its behavior. The first is that vi is a modal editor. A mode is like an environment. Different modes in vi interpret the same key differently. For example, if you’re in insert mode, typing a adds an a to the text, whereas in command mode, typing a puts you in insert mode because a is the key abbreviation for the append command. If you ever get confused about what mode you’re in, press the Escape (or Esc) key on your keyboard. Pressing Escape always returns you to the command mode (and if you’re already in command mode, it simply beeps to remind you of that fact).

When you are in command mode, you can manage your document; this includes the capability to change text, rearrange it, and delete it. In insert mode, you add text directly to your document from the keyboard.

### Note

In vi, the Return key is a specific command (meaning to move to the beginning of the next line). As a result, you never need to press Return to have vi process a command.

By contrast, the other popular UNIX editor, emacs, is a modeless editor. In emacs, the A key always adds the letter a to the file. You indicate all commands in emacs by holding down the Control (Ctrl) key while pressing the command key; for example, Ctrl-C deletes a character. We’ll have a close look at emacs in Hour 12.

The second important characteristic of vi is that it’s a screen-oriented program. It must know what kind of terminal, computer, or system you are using to work with Unix. This probably won’t be a problem for you because most systems are set up so that the default terminal type matches the terminal app you’re using. In this hour, you’ll learn how to recognize when vi cannot figure out what terminal you’re using and how to fix it.
