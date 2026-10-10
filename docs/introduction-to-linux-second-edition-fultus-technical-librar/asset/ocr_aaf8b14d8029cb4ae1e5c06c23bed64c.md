graphical environment over the network, working with text editors tremendously improves network speed.

There are, as usual, multiple ways to handle the problem. Let’s see what editors are commonly available:

# 6.1.2.1 Ed

The **ed** editor is line-oriented and used to create, display, modify and otherwise manipulate text files, both interactively and by use in shell scripts.

**ed** is the original text editor on UNIX machines, and thus widely available. For most purposes, however, it is superceded by full-screen editors such as **emacs** and **vi**, see below.

# 6.1.2.2 GNU Emacs

Emacs is the extensible, customizable, self-documenting, real-time display editor, known on many UNIX and other systems. The text being edited is visible on the screen and is updated automatically as you type your commands. It is a real-time editor because the display is updated very frequently, usually after each character or pair of characters you type. This minimizes the amount of information you must keep in your head as you edit. Emacs is called advanced because it provides facilities that go beyond simple insertion and deletion: controlling subprocesses; automatic indentation of lines; viewing two or more files at once; editing formatted text; and dealing in terms of characters, words, lines, sentences, paragraphs, and pages, as well as expressions and comments in several different programming languages.

*Self-documenting* means that at any time you can type a special character, Ctrl+H, to find out what your options are. You can also use it to find out what any command does, or to find all the commands that pertain to a topic. *Customizable* means that you can change the definitions of Emacs commands in little ways. For example, if you use a programming language in which comments start with `**<**` and end with `>**>`, you can tell the Emacs comment manipulation commands to use those strings. Another sort of customization is rearrangement of the command set. For example, if you prefer the four basic cursor motion commands (up, down, left and right) on keys in a diamond pattern on the keyboard, you can rebind the keys that way.

*Extensible* means that you can go beyond simple customization and write entirely new commands, programs in the Lisp language that are run by Emacs’ own Lisp interpreter. Emacs is an *online* extensible system, which means that it is divided into many functions that call each other, any of which can be redefined in the middle of an editing session. Almost any part of Emacs can be replaced without making a separate copy of all of Emacs. Most of the editing commands of Emacs are written in