code itself? ispell will likely flag as misspelled odd function and class names, and this could become annoying after a while. There is a value menu for this variable: a choice you might want to try is “exclusive”. Setting the variable to this value restricts ispell to spell checking only comments. This would be useless in ordinary text files, but it could be set that way on a per-session basis.

# ## Flyspell

Recent Emacstrees come with an automatic on-the-fly spell checker called Flyspell, written by Manuel Serrano. XEmacs users can find it in the text-modes package.

This mode highlights every word that ispell regards as misspelled as you type. It doesn't make you stop and correct a highlighted word, but if you want to deal with one, clicking mouse button 2 displays a menu of choices. These are the same words that would have appeared in the Choices window when using the default ispell interface.

If you would like to enable this mode on an optional basis, so that the mode would be active only when manually enabled, insert these lines in your ~/.emacs file:

```
```
(autoload 'flyspell-mode 'flyspell "On-the-fly spelling checking" t)
(autoload 'global-flyspell-mode 'flyspell "On-the-fly spelling" t)
```
```

After these two lines have been evaluated (Ctrl-x Ctrl-e), or Emacs has been re-started, press M-x and type

```
```
flyspell-mode
```
```

to enable the mode. The command is a toggle. In other words, the same command will turn Flyspell off.

If you try it out and want to use it in every Emacs buffer, insert this line instead:

```
```
(global-flyspell-mode t)
```
```

Flyspell was written with extensive Customize support. You might find the default behavior distracting, but settings can be changed to make the mode less intrusive. You can set it up so that duplicate words aren't highlighted, and you can even give it a greater time delay. More delay forces Flyspell to wait a configurable amount of time before highlighting a word, lessening the feeling that Flyspell is looking over your shoulder and urging you to correct these errors right now!

You can access this Customize buffer by pressing M-x and typing

```
```
customize-group
```
```

Respond to the prompt with

```
```
flyspell
```
```