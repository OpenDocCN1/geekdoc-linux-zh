# **Finding Installation Instructions**

If you want to learn how to install one of the more prominent Info-documented packages (such as Gnus), just press Ctrl-h i and read the instructions in the relevant Info manual. The smaller and/or more obscure packages are internally documented.

One slight drawback of Emacs (and XEmacs) is that many interesting and useful modes and packages are installed, but the supplied documentation (the Info files) covers only the larger and most-used packages, such as Dired, Gnus, and Ediff.

The Package Finder is an effective way to browse the Commentary sections of the packages supplied with Emacs. Press Ctrl-h p to bring up a Finder window (or select Find Emacs Packages from the Help menu). A buffer listing categories of packages appears. Click the second or middle mouse button on a category to see a Finder category window, as shown in Figure 12.1.

The Lisp files listed in the second window can be clicked on to access a third window, one containing the actual Commentary section of the file. In most cases, this documentation is sufficient to get you started using the package.

Another way to learn about packages is to take a look at the actual Lisp files. They can be found in the /_prefix/share/[version-number]/lisp directory and in various categorized subdirectories under it. Sometimes a package's Commentary section is scanty. The actual Lisp code can be a useful source of information.

![](bbox=[0.2, 0.6, 0.96, 0.91])

**Figure 12.1 Finder Windows**