A file or other text open in Emacs is held in its own area called a *buffer*. By default, the current buffer appears in the large area underneath the menu bar. To write text in the buffer, just type it. The place in the buffer where the cursor is at is called *point*, and is referenced by many Emacs commands.

The horizontal bar near the bottom of the Emacs window and directly underneath the current buffer is called the *mode line*; it gives information about the current buffer, including its name, what percentage of the buffer fits on the screen, what line point is on, and whether or not the buffer is saved to a file.

The mode line also lists the modes active in the buffer. Emacs *modes* are general states that control the way Emacs behaves---for example, when *Overwrite* mode is set, text you type *overwrites* the text at point; in *Insert* mode (the default), text you type is *inserted* at point. Usually, either *Fundamental* mode (the default) or *Text* mode will be listed.

You can make the menu bar appear or disappear by toggling *Menu bar* mode. Typing **F10** to activate the menu pull-downs works whether *Menu bar* mode is on or off; if it's off, the menu choices will appear in a new buffer window.

+   • To turn off the top menu bar, type:

```
M-x menu-bar-mode RET
```

(If the menu bar is already turned off, this command will turn it on.)

The *echo area* is where Emacs writes brief status messages, such as error messages; it is the last line in the Emacs window. When you type a command that requires input, that input is requested in this area (and when that happens, the place you type your input, in the echo area, is then called the *minibuffer*).

Emacs commands usually begin with a Control or Meta (Escape) key sequence; many commands begin with the **C-x** sequence, which you type by pressing and holding the **CTRL** key and then pressing the **X** key (see section *Typographical Conventions*).

Because Emacs is different in culture from the editors and approach of the Microsoft Windows and Apple MacOS world, it has gotten a rather unfounded reputation in those corners that it is odd and difficult to use. This is not so. The keyboard commands to run its various functions are designed for ease of use and easy recall.

For example, the *find-file* function prompts for the name of a file and opens a copy of the file in a new buffer; its keyboard accelerator is **C-x C-f** (you can keep **CTRL** depressed while you press and release the **X** and **F** keys).

You can run any Emacs function by typing **M-x** followed by the function name and pressing **RET**.

+   • To run the *find-file* function, type:

```
M-x find-file RET
```

This command runs the *find-file* function, which prompts for the name of a file and opens a copy of the