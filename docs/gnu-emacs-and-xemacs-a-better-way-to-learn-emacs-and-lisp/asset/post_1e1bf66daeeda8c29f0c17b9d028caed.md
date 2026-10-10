
![](img/c8827ea52a0796def3f6891892ed9d3a_305_0.png)

Figure 15.2 A Partially Folded Buffer

# Keyboard and Menu Commands

The default prefix for Folding mode commands is Ctrl-c @, a prefix I refuse to use. Casting about for a superfluous Emacs keybinding to co-opt as a prefix for Folding mode, I happened across Ctrl-v. The default binding runs the scroll-up command, which also happens to be the command called by the Page Up key. Since I never use Ctrl-v, preferring single keystrokes when possible, Ctrl-v seemed like a good candidate. If you like to do the same, you first need to unset the current binding with this line in your `~/.emacs` file:

```elisp
(define-key global-map [(control v)] nil)
```

This line needs to be earlier in the `~/.emacs` file than your Folding mode initialization lines. Now you are free to assign a new meaning to the Ctrl-v prefix. This can be done with Customize. Bring up the Folding Group Customize buffer by pressing M-x and typing

`customize-group`

When prompted, type

`folding`

Several folding settings can be changed in the resultant Customize buffer. The default prefix key is the first setting.

But since you've been mucking around in your `~/emacs` file anyway, instead of using Customize, you can add one more line directly after the `define-key` line just shown that will change the prefix for good:

```elisp
(defconst folding-mode-prefix-key (control v))
```

Even the menus will pick up this change, because they are generated from scratch each time Folding mode is started.

Figure 15.3, a screen shot of the Fld menu after this change has been made, illustrates the numerous folding-related commands that are available.

If you retained the default Folding mode prefix, each command would be prefixed with Ctrl-c @ rather than Ctrl-v.

Spend some time with `folding.el` after starting Folding mode, and you will develop a feel for navigating through a folded file. Creating your own file isn't difficult as long as you remember to keep the opening and closing fold-markers balanced.

Folding mode has built-in support for the particular commenting characters used by most programming languages. Notice how the fold indicators in Figure 15.2 are prefixed with semicolons (the Emacs Lisp comment character), but the mode still recognizes the folds. Braces prefixed with a double forward slash (signifying C++ comments) will be recognized as folds in a C++ source file. New comment characters can be added to the list with a statement such as this:

```elisp
(folding-add-to-marks-list 'major-mode *e({[`"*e{]}]`*) )
```

| Command                     | Shortcut |
|-----------------------------|----------|
| Enter Fold                  | (C-v x)  |
| Exit Fold                   | (C-v X)  |
| Show Fold                   | (C-v S)  |
| Hide Fold                   | (C-v H)  |
| Show Whole Buffer           | (C-v G)  |
| Fold Whole Buffer           | (C-v G)  |
| Show subtree                | (C-v +)  |
| Hide subtree                | (C-v -)  |
| Display fold name           | (C-v =)  |
| Move previous               | (C-v |)  |
| Move next                   | (C-v SP) |
| Pick Fold                   | (C-v P)  |
| Fold/ry region              | (C-w B)  |
| Open or close folds in region | (C-v F) |
| Open folds to top level     | (C-v L)  |
| Comment text in fold        | (C-v >)  |
| Convert for printing/Temp buffer) | (C-v D) |
| Convert to major-mode folds | (C-v 2)  |
| Move comments inside folds in region | (C-w /) |
| Insert folding URL reference | (C-v )   |
| Toggle enter and exit mode  | (C-v )   |
| Toggle show and hide        | (C-v )   |
| Folding mode off            | (C-v )   |

![](img/c8827ea52a0796def3f6891892ed9d3a_306_0.png)

This line is for an imaginary major mode that uses the @ character as its comment indicator.

If you would like to see if a particular language is supported, press the “help-on-variables” help key, Ctrl-h v.

Respond to the prompt with

```elisp
folding-mode-marks-alist
```

A window opens, displaying the numerous comment characters that Folding mode recognizes.

# An Interface to Online Dictionaries

The Dict project (http://www.dict.org) has made available a free client/server dictionary system for computer users. It works by employing a server daemon running as a background process that handles requests from client software such as dict, which is part of the distribution.

Dict is a command-line program. You type `dict word`, and the word is passed to the dictd server, which looks it up in one or more dictionary files that are compressed with a specialized compression program called dictzip. The definition is in turn passed to a pager such as less, where the definition can be read. This entire process is near-instantaneous.

The compressed dictionary files from which dict plucks definitions are all public-domain files, including an unabridged Merriam-Webster dictionary circa 1913 and the complete WordNet database. Others include a gazetteer, a Bible dictionary, and two compendiums of computer terms.

These dictionary files can be either on a remote dict server on the Internet or local files on your own machine. Linux distribution packages are available for the client, the server, and the dictionary files.

The Dict system is worth using on its own, but it wasn't long before some Emacs users began to write modes that would allow access to these dictionaries from within Emacs. One such user was Torsten Hilbrich; he wrote a feature-filled mode called `dictionary.el`. Rather than act as an Emacs front end to the dict client program, this mode takes its place and contacts the dict server directly.

# Dictionary.el Installation

Installation consists of unpacking the `dictionary-1.2.1.tar.gz` file, copying the ".el" files to your site-lisp directory, and byte-compiling the files. These lines pasted into your `~/.emacs` file will activate the mode:

```elisp
(auto-load 'dictionary-search "dictionary"
  "Ask for a word and search it in all dictionaries" t)
(auto-load 'dictionary-lookup-definition "dictionary"
  "Search the word at point in all dictionaries" t)
(auto-load 'dictionary-match-words "dictionary"
  "Ask for a word and search all matching words in the dictionaries" t)
(auto-load 'dictionary "dictionary"
  "Create a new dictionary buffer" t)

(global-set-key [(control c) (d)] 'dictionary-lookup-definition)
(global-set-key [(control c) (s)] 'dictionary-search)
(global-set-key [(control c) (m)] 'dictionary-match-words)

(setq dictionary-server "localhost")
```

The last line makes your machine the default dictionary server. If you want to use a remote server, substitute the server’s IP address for "localhost". The keybindings can be changed to suit your setup.

Dictionary mode offers several function commands. `dictionary-lookup-definition` looks up the word at your cursor location and then opens a Dictionary buffer and displays the definitions that were found. A variation called `dictionary-search` displays the word at point in the minibuffer, allowing you to edit it before pressing Enter. `dictionary-match-words` prompts you for a partial word and then displays lists of words containing the pattern, sorted by dictionary. Each word in the list is a clickable link that fetches the definition.

Figure 15.4 shows a typical Dictionary window.

At the top of the Dictionary window are several mouse-activated buttons that run the various Dictionary mode commands; the results appear in the window.

An empty Dictionary window appears if you press M-x and type

`dictionary`

![](img/c8827ea52a0796def3f6891892ed9d3a_309_0.png)

You can use the empty Dictionary window to access the command buttons.

One of the buttons in the Dictionary window can be used to select the default dictionary, which can be changed at any time. Figure 15.5 shows the menu of choices brought up by this button.

Dictionary mode is a great aid for the writer. Not only can you use `ispell` to check a word’s spelling, but with this mode, you can refer to definitions quickly.

![](img/c8827ea52a0796def3f6891892ed9d3a_309_1.png)
