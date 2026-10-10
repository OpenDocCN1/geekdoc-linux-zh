are usually built into the new package, causing a new group or subgroup to appear in the Customize buffers.

Any serious Emacs user will eventually absorb more than a little of the Lisp language. Using Customize lets you become productive with Emacs quickly, without the necessity of learning any Lisp until you feel ready.

# # How Customize Works

Any Emacs package contains a number of variables that can be changed via Lisp statements in an `~/.emacs` initialization file. If the developer “wraps” those variables in a defined way, Customize can find and incorporate them when Emacs starts up, as long as the package is in Emacs’ load-path.

> Emacs finds Lisp files only if they are in a directory contained in a list called the **load path**. The default load-path includes the native Emacs Lisp directories (part of the Emacs installation). One of these installed directories, the site-lisp directory, is empty when Emacs is first installed. This is the directory in which extra Lisp files and packages should be installed. Chapter 12 describes how to add directories to the load-path.

![](bbox=[0.88, 0.36, 0.99, 0.51])

When Emacs is started various optional packages are loaded via statements in the `~/.emacs` file. If the packages have been written with Customize support variables are created as the package is loaded. These variables add package-specific settings which the Custom library reads and translates into a Customize interface for the package whenever a Customize buffer is created. This means that every new Custom-enabled Emacs package you install will become part of the Customize interface, which is available on the menu bar and through direct M-x minibuffer commands.

The Customize interface organizes the many changeable options in a hierarchical tree-like arrangement that can be expanded and collapsed. Options are contained within groups and subgroups; this makes particular options reasonably easy to find.

Figure 4.1 shows a typical Custom session to help make this clear.

The + signs to the left of the group names can be toggled with the second or third mouse button. This action expands the group to display either expandable subgroups or individual options.

Figure 4.2 shows a single option, the default face.