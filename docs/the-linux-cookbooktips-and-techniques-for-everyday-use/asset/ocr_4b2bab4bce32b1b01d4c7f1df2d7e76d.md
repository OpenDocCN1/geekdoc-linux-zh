+   • To type the line `Emacs ist spa@ss!` in the current buffer, type:

```
M-x iso-accents-mode RET
Emacs ist spa"ss!
```

In the event that you want to type the literal key combinations that make up an accented character in a buffer where you have ISO Accents mode on, type the prefix character twice.

+   • To type the text ` ' o ` (and not the accent character ó) in a buffer while ISO Accents mode is on, type:

```
' ' o
```

*NOTE:* GNU Emacs has recently added a number of internationalization functions. A complete discussion of their use is out of the scope of this book; for more information on this topic, see section `International Character Set Support' in *The GNU Emacs Manual*.

# 11.3 Running a Vi Tutorial

```
@sf(Debian): `nvi'
@sf(WWW): ftp://mongoose.hostic.com/pub/nvi.tar.gz
@sf(WWW): http://www.cs.cmu.edu/~vaschelp/Editors/Vi/
```

The Vi editor comes with a hands-on, self-paced tutorial, which you can use in vi to learn how to use it. It's stored as a compressed file in the `/usr/doc/nvi' directory; copy this file to your home directory, uncompress it, and open it with vi to start the tutorial.

+   • To run the vi tutorial, type the following from your home directory:

```
$ cp /usr/doc/nvi/vi.beginner.gz . RET
$ gunzip vi.beginner RET
$ vi vi.beginner RET
```

*NOTE:* An advanced tutorial is also available in `/usr/doc/nvi'.