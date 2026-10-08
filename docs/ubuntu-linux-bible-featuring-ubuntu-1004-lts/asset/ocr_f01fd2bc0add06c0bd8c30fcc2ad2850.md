# Part II: Ubuntu for Desktop Users

installed or uninstalled. For example, the dpkg -l emacs command should list all of the pack- ages that have the string emacs in their package name. Let's try to:

```
$ dpkg -l emacs
No packages found matching emacs.
```

Well, that seems odd because I'm actually typing this in Emacs on my Ubuntu system. The prob- lem is that any argument that you supply to dpkg is used as a pattern match, and there are apar- no packages installed on my system whose exact name is emacs. Let's try again, using a standard Linux wildcard to say that you want to list any packages with a name that begins with emacs, as in the following example:

```
$ dpkg -1 'emacs*
Desired=Unknown/Install/Remove/Purge/Hold
Status=Not/Installed/Config-files/Unpacked/Failed-config/\
Half-Installed
| Err?=(none)/Hold/Reinst-required/X-both-problems \
  (Status,Err: uppercase-bad)
|| Name Version Description
++-------------------------------------------------------------
ii emacs-common 2.05b-1 a client/library for Chess
ii emacs-pieces 2.05b-1 XPM images of chess pieces
ii emacs-goodies-el 26.4-1 Miscellaneous Emacs add-ons
un emacs-goodies-extra-el <none> (no description available)
ii emacs21 21.4a-ubuntu2 The GNU Emacs editor
ii emacs-bin-common 21.4a-ubuntu2 The GNU Emacs shared...
ii emacs-common 21.4a-ubuntu2 The GNU Emacs shared...
un emacs-el <none> (no description available)
un emacs-nox <none> (no description available)
un emacs-sensen <none> (no description available)
un emacs-common 1.4.17 Common facilities for ...
```

That's more like it! Note that when using wildcards in a dpkg specification, you have to protect them from expansion on the command line by enclosing your dpkg wildcard specification within quotation marks of some sort.

The previous output showed some Emacs packages, but I could swear that there were others on my Ubuntu system. Let's try a more general wildcard that searches for packages that contain the string emacs anywhere in their names:

```
$ dpkg -l '*emacs*
Desired=Unknown/Install/Remove/Purge/Hold
Status=Not/Installed/Config-files/Unpacked/Failed-config/\
Half-Installed
| Err?=(none)/Hold/Reinst-required/X-both-problems \
  (Status,Err: uppercase-bad)
|| Name Version Description
```

684