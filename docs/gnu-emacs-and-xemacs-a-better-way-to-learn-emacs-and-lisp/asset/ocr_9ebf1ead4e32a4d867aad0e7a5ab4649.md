An advantage of require is that the function first checks to see if a file has already been loaded; if it has, require does nothing. This prevents a file from being loaded more than once in a session.

require is often used in a Lisp file to make available features existing in another file. The difference between the require and autoload functions is that autoload loads just the name of the file and its dostring into memory, deferring actual loading until an explicit request is made.

The choice of which of the three functions to use is normally up to the package author. The commented-out documentation in the source file usually provides sample lines that can be inserted in your ~/.emacs file. If you have trouble convincing a package to load or autoload, it is worthwhile to try one of the other functions.

# ## Deriving One Mode from Another

Mode derivation is a time-saving technique. Here's a common situation: You need a mode that makes editing a certain type of file easier. A mode designed for another sort of file is almost what you need, and it seems a shame to start from scratch. You can derive one mode from another, retaining the core functionality of the old mode but changing certain features so that the new mode works the way you need it to. It helps prevent that "Am I reinventing the wheel?" feeling.

What makes this possible is a Lisp package called define-derived-mode. It has a simple syntax:

```
```
(define-derived-mode new-mode's-name old-mode's-name mode-line-string
docstring
expression-1
expression-2
etc.)
```
```

Here's an example from gametree.el, a file bundled with the Emacs game modes:

```
```
(define-derived-mode gametree-mode outline-mode "GameTree"
"Major mode for managing game analysis trees.
Useful to postal and email chess (and, it is hoped, also checkers, go, shogi, etc.). players, it is a slightly modified version of Outline mode.

\\{gametree-mode-map}"
(auto-fill-mode 0)
(make-variable-buffer-local 'write-contents-hook)
```
```