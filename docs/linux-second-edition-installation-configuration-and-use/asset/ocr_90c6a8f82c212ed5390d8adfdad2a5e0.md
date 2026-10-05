```
(car (current-input-mode))
(nth 1 (current-input-mode)) 0
(global-set-key [delete] 'delete-char) ;Del: delete character
(global-set-key [home] 'beginning-of-line) ;Home: beginning of line
(global-set-key [end] 'end-of-line) ;End: end of line
```

Information on the everlasting problem of Back-space and Del can be found on page 243. If you are interested in more advanced Emacs configuration, you need to read about Emacs Lisp programming. Subsequently, this is described in a separate chapter from page 569 onward.

Current versions of GNU Emacs and XEmacs support input and processing of Asian and other foreign language special characters through the new Multilingual Enhancement (in short, MULE). However, this extension is not yet as mature as other Emacs functions. In the long run, Emacs will be adapted to Unicode. As long as you are happy with common 8-bit character sets (ISO Latin character sets), you do not need MULE. In this chapter, MULE is not.

# Loading and saving texts, quitting the program

Emacs is started by entering emacs xemacs. When you are working under X and Emacs is properly installed, it will automatically appear in its window with menus and scroll bars.

When you specify one or more file names when starting the program, the files are automatically loaded. Search patterns are allowed: emacs Makefile *.C *.h loads the Makefile together with all * and *. in the current directory. Independently of this, you can use Ctrl+X Ctrl+X Ctrl+F filename Return to load files at a later stage.

To save a modified file, use the keyboard command Ctrl+X Ctrl+S. If you want to quit Emacs use Ctrl+X Ctrl+C. If at that point Emacs detects any file that has not been saved, a safety confirmation request appears to ask you whether you really want to quit Emacs without saving. If you want to discard your changes, answer this request with arrow. You can also save the file under a different name by means Ctrl+X Ctrl+W filename_name.

If you use Emacs on a text console, you can temporarily leave the program with Ctrl+Z. With fg you can resume your work. (Under X, Ctrl+Z merely reduces the window to an icon.)

# Loading and saving files, terminating Emacs

```
Ctrl+X Ctrl+F load file (find)
Ctrl+X I insert file into existing text
```