
Its value is 70

Automatically becomes buffer-local when set.
This variable is safe as a file local variable if

its value

satisfies the predicate 'integerp'.
Documentation:

Column beyond which automatic line-wrapping should
happen.

Interactively, you can set the local value with <Ctrl+X>
f

You can customize this variable.

Click on the underlined text customize and you can use a buffer to change the value of this variable.

The most convenient keystroke method to set a specific customizable variable is by typing <Alt+X> set-variable. This reads the variable name with the minibuffer (with completion), and then reads an elisp expression for the new value that you type in the minibuffer a second time (you can insert the old value into the minibuffer for editing via <Alt+N>). For example:

```
<Alt+X> set-variable <ENTER> fill-column <ENTER> 75 <ENTER>
```

sets fill-column to 75.

<Alt+X> set-variable is limited to user options, customizable variables, but you can set any variable with an elisp expression like this:

```
(setq fill-column 75)
```

To execute such an expression, type <Alt+;:> (eval-expression) and enter the expression in the minibuffer. Alternatively, go to the *scratch* buffer, type in the expression, and then type <Ctrl+J>.

Setting variables this way affects only the current emacs session. The only way to alter the variable for future sessions is to put the alteration as a Lisp statement in your initialization file.

## 3.3.13.3 Init File Syntax

Your GNU emacs system's init file, ~/.emacs, contains elisp expressions. Each elisp expression consists of a function name followed by arguments, all surrounded by parentheses. For example:

```
(setq fill-column 60)
```

calls the function setq to set the variable fill-column to 60.
You can set any Lisp variable with setq, but with certain variables setq won't work.
The second argument to setq is an expression for the new value of the variable. This can be a constant, a variable, or a function call expression. In your ~/.emacs file, constants are used most of the time. They can be:

- Numbers: Numbers are written in decimal, with an optional initial minus sign.
- Strings: Lisp string syntax is the same as C string syntax with a few extra features. Use a double-quote character (") to begin and end a string constant.
- Characters: Lisp character constant syntax consists of a ? followed by either a character or an escape sequence starting with \.
- True: t stands for "true."
- False: nil stands for "false."
- Other Lisp objects: Write a single quote (') followed by the Lisp object you want.

## 3.3.13.4 Keystroke Abbreviations or Abbrevs

Just like an ordinary language abbreviation, an abbrev is a word which expands, when you insert it, into a usually expanded or enlarged string of text. Abbrevs are defined by the user to expand in specific ways. For example, you might define Bob as an abbrev expanding to Better off built. Then you could insert Better off built into the buffer by typing Bob <Space>.

A second kind of abbreviation facility, which we do not show examples of here, is called dynamic abbrev expansion. You use dynamic abbrev expansion with an explicit command to expand the letters in the buffer before the point by looking for other words in the buffer that start with those letters.

Abbrev expand only when Abbrev mode, a buffer-local minor mode, is enabled. Disabling Abbrev mode does not cause abbrev definitions to be forgotten, but they do not expand until Abbrev mode is enabled again. The command <Alt+X> abbrev-mode toggles Abbrev mode; with a numeric argument, it turns Abbrev mode on if the argument is positive, off otherwise.

You can define abbrevs interactively during the editing session, irrespective of whether Abbrev mode is enabled. You can also save lists of abbrev definitions in files, which you can then reload for use in later sessions.

### 3.3.13.4.1 Defining Abbrevs

The following are ways of defining and managing abbrevs: <Ctrl+X> a g

Define an abbrev, using one or more words before point as its expansion (add-global-abbrev).
