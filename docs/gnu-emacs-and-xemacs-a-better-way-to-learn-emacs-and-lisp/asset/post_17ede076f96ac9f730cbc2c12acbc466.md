
short tutorial in generating a useful backtrace in the file *DEBUG*, which can be found in the /etc directory of your Emacs installation.

Try not to confuse bug reports with comments on how you think Emacs should work. The latter are matters of opinion that might be appropriate in an informal newsgroup discussion but aren't the sort of things the maintainers are excited about receiving.

## Lisp Debugging Tools

If you aren't interested in Emacs-Lisp programming, you might consider skipping the remainder of this chapter. However, the next section can be used to troubleshoot malfunctioning Lisp files (such as your ~/.emacs file) even if you don't know much Lisp.

This section is introductory in nature, intended to offer an overview of the debugging solutions provided with Emacs. The following material gets you started in debugging, but you'll need to consult one of the freely available Lisp Reference Info manuals for a detailed account.

GNU Emacs is not distributed with the Info manual; you can find a copy on this book's CD-ROM in the directory /cdrom/docs/lisp. The XEmacs version of the Lisp reference is included in the standard XEmacs package.

### The Built-in Debugger

Since it would interfere with normal editing, the built-in Lisp debugger is by default disabled in non-Lisp buffers. When the major mode is Emacs-Lisp mode (which should be automatic if the file name suffix is .el), the debugger will be ready to run, at least for GNU Emacs users. XEmacs is (as usual) slightly different; look for several debugging-related items on the Emacs-Lisp menu. The most-used item is “Debug on error”. Click on the check box next to this item to enable error debugging.

With error debugging turned on, a Backtrace buffer is created when an error is encountered during the evaluation of a Lisp statement or file. At the top of this buffer are lines describing the error that caused the buffer to appear.

If you would like to confine debugging to a particular function, press M-x and type

```
debug-on-entry
```

This command prompts you for a function name. While this command is in effect, the debugger is invoked each time the function is called. Disable the command by pressing M-x and typing `cancel-debug-on-entry`.

If you have a Lisp file that won’t run at all, skip ahead to the later section “Lisp Syntax Problems”.

### Debugger Mode and the Backtrace Buffer

The Backtrace buffer displays the current Lisp runtime stack (see the following Note). The buffer’s lines are in reverse chronological order; you can read them from bottom to top to see what the Lisp interpreter was doing as it approached the error, which is shown on the top line.

![](img/c8827ea52a0796def3f6891892ed9d3a_478_0.png)

> The word *stack* is used by computer programmers to refer to a data structure for storing items. In Emacs Lisp, the items form linked lists, each list pointing to its predecessor and successor.

The Backtrace Buffer has its own major mode, called Debugger mode. This mode can be used to “step” you way through a Lisp file or code block, slowing the evaluation process so that you can see how the control flows at each stage. The keyboard is remapped so that characters execute debugging commands, similar to the way Dired and Gnus commands are assigned keys.

I’d be venturing rather far afield from the purpose of this book if I detailed the usage of the internal debugger and its powerful and versatile alternative, Edebug. If you are interested in pursuing this subject further, I recommend that you read the relevant sections in the Emacs or XEmacs Lisp Reference.

### Debugging Your `.emacs` file

When Emacs encounters an error while loading your `~/.emacs` file, it simply stops and generates an error message. You end up with a default Emacs running as if you had started it with the command `emacs -q`. Naturally, you wonder which line of the file is causing the problem. One way to find the error is to load the `~/.emacs` file just as you would any other file and evaluate the file statement by statement, using Ctrl-x Ctrl-e after each one. This can be time-consuming if the file is very large, and `.emacs` files can grow to be quite lengthy!

Another approach is to start Emacs with this command-line switch:

```
emacs --debug-init
```

The equivalent XEmacs command differs by one hyphen:

```
xemacs --debug-init
```

This switch sets the variable *debug-on-error* to *t*, meaning that at the first error, a Backtrace buffer is generated.

In Figure 22.5, you can see that Emacs balked at loading a function it had never heard of. There is one extra hyphen in this line:

```
(setq-default-frame-alist '(menu-bar-lines . 1) (cursor-type . bar))
```

That first hyphen completely confused the Emacs Lisp interpreter. Emacs expected to find a function, and, as is typical of computer programs, it couldn't see that the name of a real function, *setq*, was buried in the statement. The line should read as follows:

```
(setq default-frame-alist '(menu-bar-lines . 1) (cursor-type . bar))
```

If you look at the next line in Figure 22.5, you can see how the human error was encouraged by the presence there of a completely different function, *setq-default*.

![](img/c8827ea52a0796def3f6891892ed9d3a_479_0.png)

Figure 22.5 Debugging Emacs

The debugger isn't quite so helpful if it finds unbalanced parentheses. It tells you that you have a parenthesis problem, but not where it is. The next section outlines some techniques for tracking down a stray parenthesis.

## Lisp Syntax Problems

One of the most common errors in a Lisp file is unbalanced parentheses. The Lisp interpreter relies on these characters when deciding the boundaries of a list or statement. A missing or superfluous parenthesis can destroy any meaning a file was intended to have.

Three of the features of Emacs-Lisp mode can be helpful in this situation. Parenthesis matching, automatic indentation, and function-traversal commands can all be used to chase down these elusive and troublesome characters.

The first thing to do is make sure parenthesis matching is turned on. GNU Emacs enables this option by default, whereas XEmacs doesn't; toggle it on from the Options menu if you need to. Place point next to opening and closing parentheses, and make sure they match their proper opposites. This isn't hard to do with simple functions and statements, but in more complicated expressions, you might try the following alternatives.

The key command Ctrl-M-e takes point to the end of a function definition. With point at the beginning of a definition, see if the command takes you to the end; if it doesn't, you have narrowed down at least one problem to that area.

Another strategy to try is to insert an extra opening parenthesis at the beginning of the file or an extra closing parenthesis at the end.

If you put an extra opening parenthesis at the beginning, you can now place point just before that parenthesis and press Ctrl-M-f. This command moves point forward to the other end of a possibly unbalanced expression. Remove the extra parenthesis you added and press Ctrl-M-f again.

You can also work from the end of a file in the same manner, inserting an extra closing parenthesis and using Ctrl-M-b to move backwards over a possibly unbalanced expression.

A simpler method is to start at the beginning of the file and press Ctrl-M-f. Hold the keys down until an error is signaled. Point in most cases will be close to the unbalanced parenthesis.

The command Ctrl-M-q is used in Emacs-Lisp mode to indent an entire balanced expression. You can use this on various expressions and see what gets indented.

Possibly more or fewer lines than seems correct will be affected by the command, a possible clue to a trouble spot. The command is syntax-driven; the only way it determines what to indent is by the arrangement of parentheses. If the parentheses are unbalanced, the indentation is obviously wrong. Use the Ctrl-x u (Undo) command to restore the previous indentation if you need to.

Here’s another technique you can try: Select a self-contained region, such as a function definition, and evaluate just that region (you can find the command on the Emacs Lisp menu). If an error occurs, you know where to look for it.

If you despair of finding an error, there is always the labor-intensive method of commenting out sections one by one until what remains will run.

## Conclusion

The developers of Emacs have provided several methods of getting out of situations that seem at first glance insoluble. They have also supplied a variety of approaches to learning more about Emacs and its modes, many of them accessible without leaving the buffer you are working on. The next chapter is about the various methods of accessing the built-in Emacs help facilities.
