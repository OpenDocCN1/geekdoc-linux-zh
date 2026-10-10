xemacs. AUCTeX is most conveniently installed for usage with GNU Emacs by using the source package, which can be found in the directory `/external/auctex/emacs`. See Chapter 12 for installation instructions. AUCTeX is useless without a complete TeX-LaTeX installation. If you lack the necessary TeX setup, and you have no interest in this sort of text processing, you might as well skip ahead to the next section.

# ### New Keybindings

The file `.emacs-keys` is filled with a variety of alternative keybindings, most of which are commented out. Just uncomment bindings that interest you, evaluate them, and try them out. Copy and paste the bindings you prefer to your `.emacs` file. The F-key bindings are particulary useful, because Emacs doesn't assign bindings to these keys by default. Multikey bindings that are awkward to type can be reassigned to F keys. This can speed up your work considerably.

# ### An `.emacs` on Macros

I've written several sample macros in the file `.emacs-mcr`. These examples show the sort of Lisp that is written out by the `save-kbd-macro` function. Read the comments, because one of the examples works only with XEmacs.

# ### A Gnu User's `.emacs`

The file `.emacs-gnus` contains several of the many variables that can be set or changed by a Gnu user. These Lisp statements can be placed either in your `.emacs` file or in a file named `.gnus`, which, like `.emacs`, should be placed in your home directory.

# ## Xemacs, GNU Emacs, and Their `.emacs` Files

It is theoretically possible to run both XEmacs and GNU Emacs, with both editors using the same `.emacs` file. I've had times in the past when that has worked for me, but inevitably the acquisition of one add-on package or another causes one of the editors to complain and malfunction. Some packages are specifically designed for GNU Emacs, and others for XEmacs. The best course to follow is to make sure that each program uses its own initialization file.

The easiest way I've found to do this is to run one of the two (preferably the least-used) with another user's `.emacs` file. I use XEmacs most of the time, so I let it use the `.emacs` file in my home directory. I created another user just so I could keep a