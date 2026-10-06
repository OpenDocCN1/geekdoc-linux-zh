# The Linux Command Line

To continue searching for the same word, press the forward slash character, press the Enter key, or you can use the n key, for next.

The substitute command allows you to quickly replace (substitute) one word for another in the text. To get to the substitute you must be in command mode. The format for the substitute command is:

```
:s/new/
```

The vim editor jumps to the first occurrence of the old text and replaces it with the new text. There are a few modifications you can make to the substitute command to substitute more than one occurrence of the:

+   - :s/old/new/g to replace all occurrences of old in a line
- :#/s/old/new/g to replace all occurrences of old between two lines numbers
- %s/old/new/g to replace all occurrences of old in the entire file
- %s/old/new/gc to replace all occurrences of old in the entire file, but prompt for all occurrence

As you can see, for a command line editor, vim contains quite a few advanced features. Since every Linux distribution includes it, it's a good idea to at least know the basics of the vim editor so that you can easily edit scripts, no matter where you are or what you have available.

# ## The emacs Editor

The emacs editor is an extremely popular editor that appeared before even Unix was around. Developers liked it so much that they ported it to the Unix environment, and now it's ported to the Linux environment. The emacs editor started life as a console editor, much like vi, but has made the migration to the graphical world.

The emacs still provides the original console mode editor, but now it also has the ability to use a graphical Windows window for editing text in a graphical environment. Normally, when you start emacs editor from a command line, it will determine if you have an X Window session and start in graphical mode. If you don't, it'll start in console mode.

This section describes both the console mode and graphical mode editors so that you'll know how to use one if you want (or need to).

# Using emacs on the console

The console mode version of emacs is another editor that uses lots of key commands to perform editing functions. The emacs editor uses key combinations pressing the Control key (Ctrl on keyboard) and the Meta key. In most PC terminal emulator packages, the Meta key is mapped to the PC's Alt key. The official emacs documents abbreviate the Ctrl key as C- and the Meta key as M-. Thus, if you enter a Ctrl-x key combination, the document shows C-x. I'll do the same here so as not to confuse you.