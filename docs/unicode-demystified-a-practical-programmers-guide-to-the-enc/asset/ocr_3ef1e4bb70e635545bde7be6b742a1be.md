In this and the following examples, assume that LANG and the LC_* variables have been exported. They must be exported because they affect the standard utilities only when they are in the environment of those utilities.

The two standard locale names are POSIX and C. They describe the identical locale, which is a generic UNIX locale; setting all the environment variables to POSIX will result in traditional UNIX system behavior. Other locale names include the abbreviated language and country in the locale name. Thus En_US and Fr_CA may locale names for locales describing English in the United States and French in Canada.

An example that was run on a system that shows POSIX.2 style localization shows the results of mixing locales:

```
$ LC_TIME=Fr_FR
$ LANG=De_DE
$ cal 1 2006
```

```
Janvier 2006
Dim Lun Mar Mer Jeu Sam
1 2 3 4 5 6 7
8 9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
```

```
$ rm NoSuchFile
rm: NoSuchFile: Verzeichnis/Datei im Pfadnamen existiert nicht.
```

On some POSIX.2 systems it is possible for users to define their own locales in addition to those provided by the system; see the definition of the localef utility on page 1438.

# The POSIX Shell

POSIX.2 specifies the syntax and semantics of a shell command language. The POSIX shell is generically named sh which is most closely based on the Korn Shell, ksh. The GNU/Linux Z Shell (Chapter 15) also resembles ksh. The POSIX shell is almost a subset of the 1988 version of ksh. Both the GNU/Linux zsh and newer versions of ksh have been designed as supersets of the POSIX shell. If you want to write shell scripts that are portable across all POSIX implementations, you should try to avoid using constructs that are not supported by the POSIX shell. Here is a brief description of some of the differences between the POSIX shell and its relatives, ksh and zsh.