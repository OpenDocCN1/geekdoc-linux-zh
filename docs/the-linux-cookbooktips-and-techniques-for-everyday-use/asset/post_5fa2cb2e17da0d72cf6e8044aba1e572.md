
## 1.2 Typographical Conventions

All recipes have at least one example that demonstrates it.

- The text that describes what the example does appears just before the example itself, and is offset from the text with a bullet, like this.
- A given recipe may have several variations; each is offset with its own bullet.
- The names of documents or users that are used in some recipes may not always reference actual documents or users on your system, but demonstrate the general principles involved. So when I show how to print a file called `resume`, you might not necessarily have a file with that name on your system, but you should understand the idea which the recipe demonstrates.

Sometimes, a terminal screen is shown to illustrate an interactive session:

```
$ Text that you actually type is displayed in a slanted font, like this. If it is a command to be typed at a shell prompt, the command is preceded with a `$` character.
```

```
Text that denotes program output is displayed in a monospaced Courier font like this.
```

```
$
```

In examples where a shell prompt is displayed, the default current working directory is omitted in the prompt and just a `$` is used; when a command outputs text and then exits, the last line of an example contains a ` $` character to denote the return to a shell prompt. Don't worry if this sounds strange to you now; all of this "shell" business is explained in The Shell.

When a command exits and returns to the shell prompt without outputting text, the final shell prompt character is omitted, and a cartouche border is not drawn around the example; this was purely an aesthetic decision.

The names of files or directories appear in the text as `file`; commands appear as command, and strings of text are typeset like `some text`. GNU INFO BUG: Note that the differences in fonts and appearance are mostly lost in the Info version.

Text you type is written like this, just as in the examples, and when a specific key on the keyboard is mentioned, its conventional name is displayed in a box. For example, RET denotes the `Return` key on the keyboard.(2)

In examples where keys are meant to be pressed and held down together, the keys are separated by hyphens; the hyphens are not meant to be literally pressed. For example, pressing the CTRL, ALT, and DEL keys and holding them down at the same time is a combination that has meaning in some operating systems (including Linux, where this keystroke means to shut down the system and reboot the computer); it is represented like this:

# CTRL-ALT-DEL

The CTRL (`Control`) key is always used in combination with another key; these combinations are denoted by C-X, where X is the second key. These combinations are read as `control-X`, where X is the name of the second key. To type one of these combinations, press and hold CTRL, press the second key, and then release both keys.

- For example, to type C-d (pronounced `control d`), press and hold CTRL, type the D key, and then release both keys.

In some applications (notably, the Emacs editor; see section Emacs), the META key is used with another key, in the same way as SHIFT; these combinations are denoted by M-X, where X is the second key. Most keyboards today don’t have a META key, even though the term is still in use; instead, press and release ESC, and then type the second key.

- To type M-c, press and release ESC, and then press and release the C key.

You can sometimes also use the ALT key for the META key. This often does not work in the X Window System, but in the console you can press and hold ALT and then type the second key just as you would with a CTRL key sequence.

- So to type M-c with the ALT key, press and hold ALT, press the C key, and then release both keys.

Both CTRL and META sequences are not case-sensitive; that is, pressing X in the last example is the same as pressing x (although x is certainly easier to type). By convention, the C- or M- prefix is always given as an uppercase letter, and the key which follows is always given as a lowercase letter.

Menu items in an application are written like Menu Item; the names of command functions are written as Function.

For aesthetic purposes, a physical space appears in the text between commands and the final RET that ends a command line, and should not be literally typed (although nothing bad will happen should you actually type this space). Where explicitly pressing the space bar is called for, that key is represented in examples by SPC.

## 1.3 Versions, Latest Edition, and Errata

@sf {WWW} : http://dsl.org/cookbook/

The Linux Cookbook is available in both hardcopy and as a machine-readable file. The latest edition of this book in etext ("electronic text") form is always available from its distribution site on the World Wide Web. This site includes the most up-to-date complete text (in both HTML and GNU Info formats), and provides a method for purchasing the latest edition of the hardcopy book at a discount.
