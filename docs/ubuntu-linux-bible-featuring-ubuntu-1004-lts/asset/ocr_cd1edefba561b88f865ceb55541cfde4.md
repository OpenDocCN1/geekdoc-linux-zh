# Part II: Ubuntu for Desktop Users

package that is present in any repository listed in your /etc/apt/sources.list file. The following is sample output from a search for emacs using aptitude:

+   $ aptitude search emacs
- acl2-emacs - A Computational Logic for Applicative Comm
- aleph-emacs - The Aleph programming language - emacs mode
- cxref-emacs - Generates latex and HTML documentation for
- emacs - The GNU Emacs editor
- emacs-chess - a client and library for playing Chess for
- emacs-pieces - XPM images of chess pieces for emacs-chess
- emacs-color-themes - Color for Emacs
- emacs-extra - emacs configuration
- emacs-goodies-el - Miscellaneous add-ons for Emacs
- emacs21 - The GNU Emacs editor
- emacs21-bin-common - The GNU Emacs editor's shared, architect
- emacs21-common - The GNU Emacs editor's shared, architect[additional output deleted]

You'll notice that the aptitude utility finds more packages than the dpkg -l command that was described earlier.

Another very convenient for searching for packages is the apt-cache utility, which is a command-line utility that features subcommands that enable you to search and manipulate the cache of packages that are installed or available for your system and the metadata that is associated with those packages. You must enable the universal repository to install the apt-cache utility can also be used to search the packages in any repository that is active in your /etc/apt/sources.list file, and find even more packages because it searches within the package name and both the short and long descriptions of all available packages, whether installed or not. The following is sample output from an apt-cache search for your forte string, emacs:

+   $ apt-cache search emacs
acl2-emacs - A Computational Logic for Common Logic: emacs interface
ada-mode - Ada mode for GNU Emacs and XEmacs
af - Emacs-like reader and composer
alaleph-emacs - The Aleph programming language - emacs mode
anjsp - A major mode to edit JSP and PSP code with Emacs
anthy-el - A Japanese input method (elish frontend)
apel - portable library for emacsen
aplus-fs-el - XEmacs for A+ development
ist - Emacs List drawing package
asnl-mode - Emacs mode for editing ASN.1 specification files
bhl - Emacs mode for converting text to HTML and LaTeX
bigloo-uede - Bigloo Unified Development Environment for Emacs
biomode - [Biology] An Emacs mode to edit genetic data[additional output deleted]

As you can see, the apt-cache and aptitude utilities are easiest to use when searching for packages and return the most verbose results.

686