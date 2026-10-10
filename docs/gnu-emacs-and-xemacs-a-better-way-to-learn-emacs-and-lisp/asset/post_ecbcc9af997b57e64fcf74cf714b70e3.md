
wouldn’t work with a certain method, even though the documentation claimed otherwise. Sometimes experimenting with another of the three loading methods can help get a mode working for you.

### Load

The most basic way to load a Lisp file is with the built-in function `load`. A `load` statement looks like this:

```lisp
(load 'file-name)
```

`load` first looks for `file-name.elc`; if it can’t find that, it looks for `file-name.el`, and if that doesn’t exist `file-name` will be used.

The disadvantage to this function is that the file is loaded immediately, even if it isn’t needed until later. Using `load` would be appropriate for a heavily-used Lisp file which needs to be available quickly. The next two methods are more commonly used due to their greater flexibility.

### Autoloading

There are probably some modes that you seldom use but that you would still like to have available when needed. Autoloading such modes is the ideal technique, because the mode isn’t loaded until you call it, with either a keystroke or a minibuffer command. `autoload` is a built-in function. An `autoload` command looks like this:

```lisp
(autoload 'follow-mode "follow")
```

This is a simple example; the complete syntax of the `autoload` command looks like this:

```lisp
(autoload function-name Lisp-file docstring interactive type [last three are optional])
```

The `follow-mode` example just shown uses just the first two of the syntax example elements. It leaves out the three optional switches, as they are unnecessary when you are using autoload on a Lisp file which is in a directory on your load-path. Autoload uses the `load` function to actually load the file when you request it, so as described above an `.elc` file is used if present.

Translated into English the above autoload statement might read like this:

> “Find an Emacs Lisp file on the load-path named `follow.elc`, `follow.el`, or `follow`, preferably the first. Find a function named `follow-mode` within the file and be prepared to load that function if the user requests it.”

If only the first two required arguments are present `autoload` considers the values of the missing arguments to be nil. In other words, there is no docstring, the function isn’t interactive, and the `type` argument refers to a function (the default).

Here are two examples from an `~/.emacs` file that loads two functions from `dictionary`-mode rather than the `entire` file:

```lisp
(autoload 'dictionary-search "dictionary"
 "Ask for a word and search it in all dictionaries" t)

(autoload 'dictionary-search-word-at-point "dictionary"
 "Search the word at point in all dictionaries" t)
```

These two expressions load functions from `"dictionary"`, which is expanded by the `autoload` function to `"dictionary.elc"`. If the function can't find a file by that name on the `load-path`, it looks for `dictionary.el` instead. The `t` at the end of the expressions is meant to make the `dictionary` function `interactive`—t meaning yes or true. This means that pressing M-x and typing

`dictionary-search`

would cause the `dictionary` search function to be loaded from `dictionary.elc`, which would result in the minibuffer prompt Search word:

### Require

Some packages are necessary for your daily work; you want them to be loaded when Emacs starts and to be quickly available thereafter. The `require` function is tailor-made for this need. A `require` expression can be as simple as this:

```lisp
(require 'clipper)
```

This function doesn't explicitly load a function or a Lisp file. It loads a `feature`, an Emacs term meaning a collection of functions and/or variables.

The full syntax is

```lisp
(require '[feature-symbol] ['file-name])
```

The second argument is optional; if it is absent the function will look for a file name with the same name as the `feature`.

In order to use `require` a statement such as this one must be present in the Lisp file:

```lisp
(provide 'clipper)
```

The function `provide` adds the `feature-symbol` given as its argument to an Emacs variable named `features`, which is a list of all available features available in the current Emacs session.

An advantage of require is that the function first checks to see if a file has already been loaded; if it has, require does nothing. This prevents a file from being loaded more than once in a session.

require is often used in a Lisp file to make available features existing in another file. The difference between the require and autoload functions is that autoload loads just the name of the file and its docstring into memory, deferring actual loading until an explicit request is made.

The choice of which of the three functions to use is normally up to the package author. The commented-out documentation in the source file usually provides sample lines that can be inserted in your ~/.emacs file. If you have trouble convincing a package to load or autoload, it is worthwhile to try one of the other functions.

### Deriving One Mode from Another

Mode derivation is a time-saving technique. Here's a common situation: You need a mode that makes editing a certain type of file easier. A mode designed for another sort of file is almost what you need, and it seems a shame to start from scratch. You can derive one mode from another, retaining the core functionality of the old mode but changing certain features so that the new mode works the way you need it to. It helps prevent that "Am I reinventing the wheel?" feeling.

What makes this possible is a Lisp package called define-derived-mode. It has a simple syntax:

```lisp
(define-derived-mode new-mode's-name old-mode's-name mode-line-string
docstring
expression-1
expression-2
etc.)
```

Here's an example from gametree.el, a file bundled with the Emacs game modes:

```lisp
(define-derived-mode gametree-mode outline-mode "GameTree"
"Major mode for managing game analysis trees.
Useful to postal and email chess (and, it is hoped, also checkers, go, shogi, etc.) players, it is a slightly modified version of Outline mode.

\\{gametree-mode-map}"
(auto-fill-mode 0)
(make-variable-buffer-local 'write-contents-hook)
```

```lisp
(add-hook 'write-contents-hooks 'gametree-save-and-back-layout!)

;;; Key bindings

(define-key gametree-mode-map "\C-c\C-j" 'gametree-break-line-here)
[etc]
```

The first line sets the scene: `define-derived-mode` is being called to make a new mode, `gametree-mode`, using `outline-mode` as a foundation. `mode-line-string` is a short, descriptive piece of text that is displayed in the mode-line—in this case, “Gametree”.

The next three lines are the docstring, the optional built-in documentation found in most well-written modes. Notice that the first line breaks prematurely (right after `name`). It’s an Emacs custom to start a docstring with a single-sentence summary on a line by itself. The apropos help facility looks for that summary line and displays it if you press `C-h l` after `gametree-mode` has been loaded. The docstring ends with an odd-looking expression beginning with two backslashes. This is a code understood by the Emacs internal help system; it means “Evaluate the expression between the curly braces, and substitute the result for this line.” If you had a buffer in `gametree-mode` and you summoned help for the mode by pressing `C-h m`, the Help buffer would look like **Figure 11.2**.

![](img/c8827ea52a0796def3f6891892ed9d3a_215_0.png)

Figure 11.2 Gametree Help

Notice how the docstring has been altered: The backslash-prefixed line is gone, and the list of keybindings (`gametree-mode-map`) has been substituted in its place. Following the docstring is the actual body of the expression, which is made up of a sequence of function definitions and/or variable declarations. The define-key function in this example uses an alternative way of showing a keybinding. Backslash escape characters are used as a substitute for the bracket-parenthesis system illustrated in the preceding chapter. This keybinding is equivalent to [(control c) (control j)].

### Modifying a Mode

Sooner or later, every Emacs user finds the thought “I wish there were a mode to make this sort of editing easier!” passing through his or her mind. Perhaps you are editing a new type of file and wish there were font locking for the file type or a new key command that would speed up a repetitious task.

I would be willing to bet that many accomplished Lisp hackers who create new modes from scratch got their feet wet by changing an existing mode. The Lisp source is freely available for nearly every mode; all you need to do is find one that comes close to what you need.

One Lisp skill that is essential if you want to get very far in adapting a mode is facility with regular expressions. They are used in one way or another in just about every mode, especially in the font-locking routines.

You need to be able to tell the font-locking engine how to recognize a particular chunk of text, and regular expressions are the only practical means to do so. Take a look at this font-locking code snipped from rmail.el:

```lisp
(defvar rmail-font-lock-keywords
  (eval-when-compile
    (let* ((cite-char "[>]")
           (cite-prefix "^A-Za-z")
           (cite-suffix (concat cite-prefix "0-9_~^\"")))
     (list '("^\\[From\\|Sender\\]:" . font-lock-function-name-face)
           '("^Reply-To:.\\$" . font-lock-function-name-face)
           '("^\\[Subject]" . font-lock-comment-face)
           '("^\\[To\\[Apparently-To\\[Cc\\[Newsgroups\\]:"
             . font-lock-keyword-face)
           [remainder of defvar statement cut])))
```

This is how the rmail Emacs mail client determines which lines to highlight. Note the numerous regular expression symbols used throughout, such as the caret (^) to
