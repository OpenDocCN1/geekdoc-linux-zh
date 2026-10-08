# KEYBOARD MAPPING 169

functions. Emacs differentiates between a global mapping that applies to all
modes and a local mapping, possibly adapted to individual modes.

Please note that many modes redefine individual keys in a local table, so
t the mapping can change between buffers and a global adaptation
possibly not be working in one particular mode. Listing 5.9 shows examples for
t adaptation of the global and one local keyboard table. Please note that the
representation of many keys differs from GNU Emacs and XEmacs; this will
probably not change in the near future.

```
; global adaptations
(global-set-key [home] 'beginning-of-line)
(global-set-key [end] 'end-of-line)
(global-set-key "C-cg" 'goto-line)
```

```
; adaptation of the LaTeX keyboard map
(defun-my-latex-mode-hook ()
(define-key Latex-mode-map '[delete] 'delete-character))
(add-hook 'latex-mode-hook' 'my-latex-mode-hook')
```

Listing 5.9 Adaptation of the keyboard map.

First, the keys [Home] and [End] are mapped in such a way that the cursor is
m to the beginning of the line or the end of the line. Emacs default
setting is that the cursor jumps to the beginning or the end of the buffer. Here,
symbolic names are used for the keys [home] and [end] Emacs maps
internally to the corresponding keys of the terminal. This allows you, by
relatively simple means, to specify a uniform keyboard mapping for different
terminals and keyboards.

Note that some key combinations, such as [Shift-F1], are only uniquely
der under X. Furthermore, a number of keys are not available on various
terminals or terminal emulations. However, Emacs includes configurations for
t most widely used terminals; in addition, the terminfo or termcap
database is used.

In the third line of Listing 5.9, the command goto-line is mapped to the
key combination until now refer to the global
keyboard table. To set these mappings, the elisp function global-set-key
is used, which you can also call interactively.

In addition to the default keys, many modes use additionally mapped keys.
These modifications are stored in a mode-specific keyboard table. All keys not
changed in that table keep their global mapping. Some special modes, such as the
dired mode, modifying the functioning of a large number of keys.

In the second part of Listing 5.9, the Del key in LaTeX mode is mapped to
what one is used from other editors. In the current version of AUCTEX, this