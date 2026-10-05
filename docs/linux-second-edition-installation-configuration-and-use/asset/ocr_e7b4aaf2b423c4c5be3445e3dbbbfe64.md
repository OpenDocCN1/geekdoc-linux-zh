# 17.3 Programming techniques

In order to give you an idea of what an Emacs configuration file looks like, a typical code section: in the four lines, a new Emacs function, jump-to-position, is defined which moves the cursor to the position previously stored in register 1. This function is assigned the keyboard shortcut `F6` for easy and efficient use.

```
```lisp
(defun jump-to-position() ;definition of a
  (interactive)
  ;new function
  (jump-to-register 1))
  (global-set-key [F6] 'jump-to-position) ;new shortcut F6
```
```

While you are editing the .emacs file, you can execute the command `Alt+X eval-buffer`. With this command, all Lisp commands in the active file are executed. The command saves you constantly restarting Emacs in order to try out a modified version of .emacs.

If there is a syntax error in .emacs, Emacs ignores the file from the faulty line onward. An error message is displayed below the status line, but it becomes invisible when you load a file at Emacs start-up. In this case, the line is used to display a message about the most recent action - for example about syntax highlighting.

In other words: a syntax error in .emacs easily goes unnoticed, and you will wonder why subsequent changes in .emacs remain without effect. The best way to track the error is to download .emacs into the editor and to explicitly execute the commands contained in it by means of `Alt+X eval-buffer`. The incorrect instruction will be identified instantly.

Another very useful command for testing single Lisp instructions is `Alt+X eval-region`. This command only executes the instructions between the marking point (`Ctrl+Space`) and the current cursor position.

# Executing Lisp code

`Alt+X eval-buffer` execute Lisp instructions in the active buffer
`Alt+X eval-region` execute instructions between marking point and cursor position

# Online help about Lisp programming

The Emacs online documentation contains a lot of useful information about Emacs programming: `F1`, `F function-name` gives a short description of the specified Lisp function. `F1`, `Tab` supplies a list of all available Lisp functions. In order for this list to be viewed, the command must be aborted with `Ctrl+G`. Then, you can switch to the buffer containing the list of functions with `Ctrl+X B *Com-*