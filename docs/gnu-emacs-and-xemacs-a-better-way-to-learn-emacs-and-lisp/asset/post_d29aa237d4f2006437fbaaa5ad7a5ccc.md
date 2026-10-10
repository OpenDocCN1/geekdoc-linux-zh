
GPL-licensed software projects. The Linux source code is another variant style. Figure 16.1 shows C code indented in the default style, and Figure 16.2 is the same code in the Linux style.

![](img/c8827ea52a0796def3f6891892ed9d3a_325_0.png)

> Default cc-mode-Style Indentation

![](img/c8827ea52a0796def3f6891892ed9d3a_325_1.png)

> Linux-Style Indentation

As you can see, the styles aren’t radically different; the brace alignment and amount of indentation vary between the styles. You can easily try any of the 11 available styles. Either press Ctrl-c or press M-x and type

```
c-set-style
```

You are prompted for a style in the minibuffer. Delete the default value and press the Tab key. A Completion window opens with a list of all indentation styles supported by cc-mode. Choose one and type its name in the minibuffer. You won’t see any change until you do one of two things: type in more code or select a region of existing code and reindent it with the M-Ctrl-l command.

This keystroke calls the command `indent-region`, which uses whichever indentation style is in effect.

After trying these various styles, you might find one you prefer over the default. You can set this variable from within a Customize Group buffer (go to the “c” group), where you will find a Default Style setting. You need to remember the exact name of the style (as it was shown in the Completion window) so that you can type it in the entry field.

Otherwise, you can use a `c-mode-hook` setting in your `~/.emacs` file, as in this example:

```
(add-hook 'c-mode-hook
  (lambda ()
    (c-set-style "name")))
```

Don’t forget the double quotes around the name of the style.

### Indenting Automatically

The Tab key has a special role in cc-mode. In a normal text-mode buffer, the Tab key inserts a configurable number of spaces (by default, eight); this simulates the behavior most people are accustomed to. In a cc-mode buffer, Tab inserts a variable number of spaces, depending on the syntactic role of the statement you are typing. This can be disconcerting if you aren’t used to it, but what the mode is trying to do is keep your code indented according to your chosen style. This lets you concentrate on the code while the indentation is adjusted for you as you type. You can see a demonstration of this by pressing the Tab key, typing something (try a function definition), and then moving the cursor back to the beginning of the line and repeatedly pressing the Tab key. You would expect the definition you typed to be pushed to the right by these tabs, but you will find that once the Tab key has indented a line to the proper column, it refuses to let you insert more. If you need to insert real tab characters, you can always use the “insert quoted literal” key command, Ctrl-q Tab.

Another useful indentation command which is not restricted to cc-mode is the “indent-for-tab” command, Ctrl-i. This command will indent a line in the proper way for the current major mode. Automatic indenting will save you more time than any other single feature of cc-mode. It just takes a little practice to let it do its work while you do yours.

## Electric Characters and Hungry Delete

These two features are turned off by default (probably to avoid scaring away skittish new users), but they both are well worth trying out. You might find one or both of these features to your liking, in which case you can turn them on permanently.

The `auto-newline` feature changes the results of typing the comma, colon, semicolon, and curly brace keys. These characters all have a certain syntactical meaning in the C and C++ languages, so cc-mode can make general assumptions about what you need after you type one of them.

A semicolon is used to terminate a statement in C, and the convention is to start the next statement on a new line. The “electric” semicolon provided by `auto-newline` in effect presses Enter for you, and point ends up at the beginning of a new line. Let’s say that your next character is a curly brace that is intended to enclose a function definition:

```
statement;|
```

As soon as you type the brace, a newline plus the proper amount of indentation is inserted. (The pipe character on the last line shows where your cursor would end up.) To turn this feature on temporarily, press Ctrl-c Ctrl-a. The same key command turns it off again.

The other optional feature is complementary to the `auto-newline` “electric” characters; it is called `hungry delete`. It increases the appetite of your Backspace and Delete keys so that they consume all spaces in their paths until either the beginning or end of a line is contacted or a nonspace character is encountered. What this does for you is speed up removal of indentation spaces when you’ve made a mistake and need to back up. It’s easy when you zippily backspacing through a row of spaces to hold down the key a little too long, inadvertently wiping out a character or two you wanted to keep. Hungry delete helps prevent this.

You can turn on this feature by pressing (while in cc-mode) Ctrl-c Ctrl-d. Turn on both of these features simultaneously by pressing Ctrl-c Ctrl-t.

If you try these two features and you want them turned on permanently, you can insert one of the following statements into your `~/.emacs` file.

For `auto-newline` only, use this one:

```
(add-hook 'cc-mode-hook
  (lambda ()
    (c-toggle-auto-state 1)))
```

This one activates `hungry delete`:

```
(add-hook 'cc-mode-hook
  (lambda ()
    (c-toggle-hungry-state 1)))
```

If you want both, this statement fills the bill:

```
(add-hook 'cc-mode-hook
  (lambda ()
    (c-toggle-auto-hungry-state 1)))
```

These `lambda` functions can be typed into one of the `cc-mode-hook` entry fields in the Customize buffer (discussed in the next section) as an alternative to plugging one of the preceding statements into your `~/.emacs` file.

You can always tell whether either of these two submodes is active by glancing at your modeline. If the mode indicator is C, both are toggled off. If the indicator is C/a, `auto-newline` is toggled on. If it's C/h, `hungry delete` is toggled on. C/ah in the modeline means that they both are active.

## Other cc-mode Variables

There was a time when developing a complete set of customized variables for cc-mode was a significant undertaking. It was done by constructing Lisp statements that redefined any of cc-mode’s numerous tweakable settings. Luckily for the user, many of these variables now have a Customize interface. If you use cc-mode frequently, it is worthwhile to scan the mode’s Customize Group buffer and see if you might want to change anything. You might guess that the group to look for would be `cc-mode`, but the name is just “c”. Press M-x and type `customize-group`.

When prompted, respond tersely with `c`. The resultant Customize buffer will look something like Figure 16.3.

## Possible Performance Problems

When you use the navigation key commands to jump from the body of a statement back to the beginning, or from a preprocessor conditional to the previous one, quite a bit of scanning and parsing are going on behind the scenes. With some coding styles, cc-mode can get lost and stalled, possibly even hanging the Emacs session. cc-mode prefers to scan forward in a file, because C and C++ can be difficult for the mode to interpret when moving backward, against the logical flow. The mode makes a leap backward, hoping to overshoot, say, the beginning of a function, and then scans forward until it is found.

There is an easy way to avoid these potential problems: Try to place the opening curly brace that begins a function definition (in C) or class definition (in C++ or Java) in the first column. Emacs and cc-mode try to encourage this by the way indentation and electric characters are set up.

![](img/c8827ea52a0796def3f6891892ed9d3a_329_0.png)

The K&R style of indentation can cause problems with function argument declarations, because this style has them beginning in the first column. Indenting argument lists one space greatly speeds up cc-mode parsing.

See the cc-mode Info files for more on this topic.

## cc-mode and Java

cc-mode can be used to edit Java code. It knows about Java syntax, commenting, and indentation, but an extension built on top of cc-mode is preferable. It's called the JDE, which stands for Java Development Environment. Read all about it in the next section.

## JDE

The Java Development Environment is one of the "big modes"; it's large and complex, but it comes with well-illustrated HTML documentation. I can only scratch the surface in this chapter's coverage of the mode, but hopefully this section will be enough to pique your interest and get you off to a good start with JDE.

JDE, like many free software projects, began with a single developer. Paul Kuncean started the project and is still the maintainer, but in recent years a sizable user community has arisen, complete with an active mailing list and many user contributions.

## Requirements and Installation

You can use any Java Development Kit with JDE, but it will need some customization to be used with kits other than one of the official JDKs from Sun Microsystems. See the later section "Customizing JDE" for details.

## GNU Emacs Installation

A GNU Emacs JDE installation requires several external Emacs packages:

- semantic
- beanshell
- elib
- eieio
- Speedbar

The Speedbar package is included with GNU Emacs, but it is a good idea to install a newer version in order to make it work with the other required packages.
