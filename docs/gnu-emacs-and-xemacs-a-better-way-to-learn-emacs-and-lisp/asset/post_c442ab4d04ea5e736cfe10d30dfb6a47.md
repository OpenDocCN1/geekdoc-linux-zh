
## Keybindings

Modes generally don't need an entirely new set of keybindings. Many of them use the `make-sparse-keymap` function to construct a local keymap, which is a set of bindings limited to the current buffer.

The `Ctrl-c` prefix is reserved for use by modes as well as for user-defined keybindings. Several characters that can follow `Ctrl-c` are reserved for use by major modes:

- `Ctrl-c Ctrl-l-[character]`
- `Ctrl-c [digit]`
- `Ctrl-c [{],<,>,], or :}`

You can be certain that if you use `Ctrl-c` followed by a letter character for your own keybindings that there will be no conflict with a major mode's keybindings.

Certain special-purpose modes aren't used for actual editing. Inserting text is not what they are intended for; thus, they can take over the keyboard completely. The `Dired` file-management mode is a good example. Dired uses many of the letter keys to perform various file operations, such as marking and deleting.

Another such mode is `dictionary` mode, an add-on that acts as an Emacs interface to a dict dictionary server. Dictionary mode is used with keybindings that allow you to look up the definition of the word at point. The definition is displayed in a new dedicated dictionary window. When this happens, the following code kicks in:

```lisp
(setq dictionary-mode-map (make-sparse-keymap)
  (suppress-keymap dictionary-mode-map)

(define-key dictionary-mode-map "q" 'dictionary-close)
(define-key dictionary-mode-map "h" 'dictionary-help)
(define-key dictionary-mode-map "a" 'dictionary-search)
(define-key dictionary-mode-map "D" 'dictionary-select-dictionary)
(define-key dictionary-mode-map "M" 'dictionary-select-strategy)
(define-key dictionary-mode-map "m" 'dictionary-match-words)
(define-key dictionary-mode-map "d" 'dictionary-search-word-at-point)
(define-key dictionary-mode-map "1" 'dictionary-previous)
```

This Lisp code starts out by creating a new variable, `dictionary-mode-map`, which starts out with the value returned by `make-sparse-keymap`. In the next line, the normal keymap is replaced using a built-in function called `suppress-keymap`. This function replaces the current keymap with the value of the argument to the function, which in this case is `dictionary-mode-map`. At this point, `dictionary-mode-map` is empty, but the following lines add keybindings to the keymap—bindings that previously were normal character-insertion commands.

In each of the lines, the last element is the name of a function defined elsewhere in dictionary.el.

Later in dictionary.el, the following line makes the new keymap active in the dictionary window but nowhere else:

```lisp
(use-local-map dictionary-mode-map)
```

### Indentation

Programming modes such c-mode, python-mode, and lisp-mode redefine indentation behavior. For example, some programmers like to be able to indent functions as a unit. The Emacs C/C++ mode (cc-mode) provides keyboard commands for this as well as the indentation of entire parenthesized or bracketed statements. Other language modes provide these features to a greater or lesser degree.

### Word Wrapping

Text-mode isn’t the only mode that can make use of auto-fill-mode. The various mail message composition packages, such as Gnus and rmail, by default load either auto-fill-mode or a related mode called adaptive-fill-mode.

The above-mentioned cc-mode uses word wrapping only within comment blocks, the areas of a source code file in which wrapping is appropriate or needed.

Later in this chapter, the concept of mode derivation will be introduced. It’s a means by which one mode can “inherit” traits from another. Several modes use this device to add features to a new mode without having to rewrite function code.

### Minor Modes

Every buffer is always in some major mode, even if it’s only fundamental mode. Usage of minor modes is optional. When one of these smaller modes is enabled, it adds something to the behavior of the dominant major mode without interfering with the major mode’s features.

An example of this is auto-fill-mode, a minor mode, in conjunction with text-mode. All text-mode does by itself is set up a few keybindings (such as M-Tab, which calls on *ispell* to complete a partially-typed word) and define a blank line as a paragraph separator. The auto-fill minor mode adds word wrapping to the basic text-mode behavior.

Any number of minor modes can be active in a buffer, but more than two or three is uncommon.

A minor mode may install a new keymap that can redefine some of the keys in the major mode's keymap. The documentation summoned by the mode help key Ctrl-h m lists the keybindings of all active modes, including minor modes.

### The Advantages of Multiple Modes

You might use a major mode for a particular type of file but find that one small feature is missing. The prospect of trying to edit the major mode's Lisp files in order to add that feature can be daunting. The mode works fine now, and you have to risk making it unusable somehow. Chances are there is a minor mode available that will add that missing capability, but if you can't find one, you can try writing your own without risking damage to the major mode files.

### Mode Hooks

The idea of providing hooks for modes is an inspired one. Imagine that a mode is some sort of material object. Imagine further that this object has hooks mounted on it on which can be hung smaller objects that change the object's behavior. That is the idea behind mode hooks: Build into a mode a facility for modifying the mode with a simple Lisp expression. This is similar to the idea of the minor mode, but the Lisp expression that hooks on to a mode hook need not be as complex as a full-blown minor mode. This is what you use if you just need to add, say, a single new keybinding to a mode.

Here is an example of a line that enables hooks for text-mode (this line was extracted from the text-mode.el file):

```lisp
(run-hooks 'text-mode-hook)
```

Now here's a line that could be in ~/.emacs that adds a hook to text-mode:

```lisp
(add-hook 'text-mode-hook 'turn-on-auto-fill)
```

The hook in this example is a simple instruction: execute turn-on-auto-fill, a built-in function that unconditionally turns on auto-fill-mode.

Mode hooks make it easy to add one or more features to a mode. Keybindings, new faces, and running an existing function can all be done with an add-hook statement.

Here's another example:

```lisp
(add-hook mail-mode-hook
  (lambda ()
    (define-key mail-mode-map [(control c) (x)] 'mail-send-and-exit)
    (define-key mail-mode-map [(control c) (c)] 'mail-cc)
    (setq fill-column 65)))
```

This one adds two new keybindings to mail-mode and changes the fill-column setting. It does this using the lambda function, which is an anonymous function, unnamed because it has no use outside this particular setq variable definition.

Notice the difference between these two examples. The first one adds a hook, so if other text-mode hooks have been defined, this one will be added to the list rather than replacing the earlier hooks. The second example is a setq variable definition, which replaces any value that mail-mode-hook might have had. Use this form when you are certain that no other hooks have been attached to the mode. Because these hooks are normally defined in the ~/.emacs file, it’s no great chore to check the file for previous hook entries pertaining to the mode in question.

### How to Associate Modes

Some modes aren’t useful unless they’re used along with one or more other Lisp libraries. The require function is used near the beginning of a Lisp mode file to force the loading of features from another file before the body of the mode is evaluated (see the following section for more about require). This is often how multile packages are constructed. The advantage to the user is that only one statement in your ~/.emacs file is needed to load the entire package. Notes-mode is a good example. The first two lines of notes-mode.el cause two related files, notes-variables.el and notes-aux.el, to be loaded before the main body of notes-mode.el is evaluated:

```lisp
(require 'notes-variables)
(require 'notes-aux)
```

Splitting a large mode into several files makes life easier for the developer. Related functions and variables can be segregated into a separate file. This also separates possible errors, making it easier to track them down.

### Different Ways to Load a Mode

Three ways of writing Lisp expressions in your ~/.emacs file activate a mode. They each have their advantages and limitations, and an add-on mode might be written in such a way that only one will work. I have encountered mode packages that
