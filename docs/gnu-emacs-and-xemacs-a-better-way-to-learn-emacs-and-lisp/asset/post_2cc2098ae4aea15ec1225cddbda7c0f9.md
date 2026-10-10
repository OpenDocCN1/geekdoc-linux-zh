
![](img/c8827ea52a0796def3f6891892ed9d3a_167_0.png)

Figure 6.5 *The Message Buffer*

The Message buffer is a record of every message or warning that Emacs generates during a session. It isn’t saved when you exit Emacs; it’s the same sort of temporary buffer as the Scratch buffer. It isn’t a bad idea to take a look at it every now and then, just to check for Lisp files that might need to be re-byte-compiled.

You can find the Message buffer on the GNU Emacs Buffers menu. Under XEmacs, select the Show Message Log entry from the Edit menu.

# Conclusion

A good way to familiarize yourself with the byte-compiler is to spend some time fooling around with it. Try deleting some `*.el` files in your `/usr/share/emacs/[version-number]/lisp` directory, first making certain that the matching `*.el` files are installed. Load the `*.el` files into Emacs, and try the byte-compilation commands discussed in this chapter. The Lisp files that are a part of your Emacs installation will byte-compile with no problems. This should give you confidence before you try byte-compiling third-party Lisp files.

The next chapter’s goal is to help you become comfortable with a crucial Lisp file—the `.emacs` initialization file. This will open the door to a multitude of possible Emacs customizations.

# PART II

# Learning to Configure Emacs with Lisp

- 9 First Steps in Customization: Your .emacs File
- 10 Changing Default Behavior
- 11 Modes, Major and Minor

![](img/c8827ea52a0796def3f6891892ed9d3a_168_0.png)

# Chapter 9: First Steps in Customization: Your `.emacs` File

- Building Blocks of the File
- Troubleshooting the File
- Backing up Your `.emacs` File
- Byte-Compiling `.emacs`
- Splitting Your `.emacs` File
- Loading the New Files
- Sample `.emacs` Files
- XEmacs, GNU Emacs, and Their `.emacs` Files

## This File Makes Your Editor Unique

If you work with Emacs for a while, you will eventually be confronted with the prospect of editing your .emacs file. Perhaps you've tried this and inadvertently ended up with a plain-vanilla Emacs that refused to even load your configuration file! This chapter shows you how this important file is put together and how to bend it to your will.

## Building Blocks of the File

Customizations of Emacs' default behavior are contained in a single Emacs-Lisp file named .emacs, which lives in your home (~) directory. This file doesn't exist in a new user's Emacs installation. It can be created from scratch by the user or indirectly via the Customize utility, when options you've changed are saved for future sessions.

> I don't recommend making numerous changes to an .emacs file in one editing session. Doing this makes it difficult to track down the source of any problems that might arise.

### Functions

An .emacs file consists of a series of self-contained functions called expressions, each one made up of a function name followed by arguments. For example:

```lisp
(global-set-key `(kbd "<f4>") 'end-of-buffer)
```

is a complete Lisp statement. It calls the built-in function `global-set-key` with arguments telling the function to make the F4 key move point to the end of the buffer. The arguments call two other built-in functions, `kbd` and `end-of-buffer`. See Chapter 6 for more about Lisp functions.

### Definitions

Much of Emacs' behavior is determined by the values stored in Emacs Lisp variables. These variables are available to the user and can be changed at any time; the most common method of changing these values is with statements in your ~/.emacs file.

A built-in function used for this purpose is `setq`, as in this example:

```lisp
(setq initial-scratch-message nil)
```

`setq` explicitly sets a variable to a value. The default value of the variable `initial-scratch-message` is `t`, or true. When the value is true, a “splash screen” appears in the Scratch buffer every time Emacs starts up. This screen contains basic information about the editor and directions for finding help. The preceding line in your .emacs file suppresses the initial message screen.

The Lisp terms `t`, meaning true, and `nil`, meaning false, are frequently found in Lisp expressions (see Chapter 6).

## Troubleshooting the File

When Emacs is starting up, it reads your .emacs file, starting at the first line and proceeding to the end. If any error is encountered, the built-in Emacs-Lisp interpreter immediately rejects the file and instead loads the default settings. A message beginning with the phrase “error in init file” appears in the minibuffer, with a reference to the line number where the first problem occurred.

## Handling Parentheses

Any Emacs user who has experimented with settings in an .emacs file has probably inadvertently broken the code at one time or another. Lisp needs the parentheses in a Lisp file or statement to balance; that is, for every opening parenthesis, there must be a matching closing one. A Lisp function often contains several nested parenthesized statements. One missing parenthesis is not necessarily noticeable to the human eye, but it can make the Lisp function make no sense at all to the Emacs interpreter. Emacs just gives up on the malformed .emacs file and reverts to its compiled-in defaults.

## Parenthesis Modes

The developers of Emacs long ago tired of manually counting stacks of parentheses. A mode called `blink-matching-paren` is by default turned on in a new GNU Emacs installation. This mode causes the parenthesis at one end of a parenthesized expression to blink whenever point is on the other end. An X Windows-specific variant called `show-paren-mode` can be turned on or off with the minibuffer command `M-x show-paren-mode`. This mode highlights the corresponding opposite parenthesis to the one the cursor is on. XEmacs has three parenthesis-matching modes that you can activate by selecting Options, Paren Highlighting. Any of these modes will help you spot unbalanced parentheses.

You can also use the key-commands `Ctrl-M-f` and `Ctrl-M-b` to move forward and backwards from one correctly parenthesized expression to another.

## Other Sources of Errors

Another potential cause of error can be a missing or superfluous single quote ('). Remember that a single quote before a list tells the interpreter that the list is not a function to be evaluated (see Chapters 6 and 7). A missing quote causes Emacs' Lisp interpreter to unsuccessfully try to link the list with a function definition, and an error occurs. Conversely, a single quote accidentally placed before a legitimate function causes Emacs to ignore and thus fail to execute the function.

There are several techniques for finding and dealing with Lisp errors. If you suspect a certain routine of problems, select the entire function or statement to focus Emacs' attention on that region only. Do this either by pressing `M-x` and typing

```
eval-region
```

or by selecting Evaluate Region from the Emacs Lisp menu. Another method of confining the evaluation is to place the cursor directly after a single Lisp expression and pressing `Ctrl-x Ctrl-e`. You might remember this from Chapter 6 as the keystroke for Evaluate Last S-expression, a function also available on the Emacs Lisp menu.

Another technique for tracking down .emacs file errors is to start Emacs in such a way that the Lisp debugger is invoked if an error occurs. Do this by using this switch when starting Emacs:

```
emacs -debug-init
```

See Chapter 22 for information about the Lisp debugger.

## Comments

Most programming languages are designed to allow the programmer to include text intended for human readers within their source code. These sections or lines are known as comments; they are used to help the programmer (and whoever else might later see the code) understand what the code is intended to do.

Comments are ignored by the compilation or interpretation software that transforms the code into a form that a computer can execute. A special character is used to inform the software that a particular line or block of code should be ignored. Surrounding or prefixing an area with this character is known as commenting out the area. Here is an example:

```lisp
;; Make F8 be "start macro", F9 be "end macro". 
;; F10 be "execute macro" 
(global-set-key [f8] 'start-kbd-macro)
```
