
```
BLT
Ham on Rye
Roast Beef
```

Figure 10-10. The sandwiches file.

```
Diner Menu for Today

Soups
-----

include(soups)

Sandwiches
-----------

include(sandwiches)
```

Figure 10-11. The menu file.

⇒ To process the file and write it to the file monday.txt, type:

```
$ m4 menu > monday.txt [RET]
```

This command writes a new file, monday.txt, as in Figure 10-12.

```
Diner Menu for Today

Soups
-----

Clam Chowder
Lobster Bisque
Vegetable

Sandwiches
-----------

BLT
Ham on Rye
Roast Beef
```

Figure 10-12. The monday.txt file.

**NOTES:** You can write more than one include file that will use your files—and these include files themselves can have inclusions of their own.

## 10.8 Using Other Text Editors

The following table describes some of the more popular or interesting text editors available for Linux, and includes information about their special traits and characteristics as well as a screen shot.

### AEE

The advanced easy editor has a pop-up menu interface and is meant to be usable with no prior instruction; includes an interface for use in X, xae.

```
DEB: aee
RPM: aee
WWW: http://mahon.cwx.net/
```

![](img/be7f02611e5cefde1a18c788fede22f7_296_0.png)

Figure 10-13. Advanced Easy Editor.

### Cooledit

Cooledit is a popular, fast text editor for use in X; its features include anti-aliased fonts, Unicode support, and extensibility via the Python programming language. It's based on the Midnight Commander's terminal editor, and it's unique in that it is unlike either Emacs or Vi.

```
DEB: cooledit
RPM: cooledit
WWW: http://cooledit.sourceforge.net/
```

![](img/be7f02611e5cefde1a18c788fede22f7_297_0.png)

Figure 10-14. Cooledit.

### DEdit

DEdit is a simple editor for use in X with GNOME installed. It can read compressed files and display Japanese characters.

```
DEB: dedit
```

![](img/be7f02611e5cefde1a18c788fede22f7_297_1.png)

Figure 10-15. DEdit.

### E3

A tiny editor (10 KB in size) with available keyboard bindings that emulate Emacs, Vi, PICO, Nedit, and WordStar.

```
DEB: e3
RPM: e3
WWW: http://www.sax.de/~adlibit/
```

![](img/be7f02611e5cefde1a18c788fede22f7_298_0.png)

Figure 10-16. E3.

### EE

Intended to be an editor that novices can begin using immediately, the Easy Editor features pop-up menus and is based on aee, described previously.

```
DEB: ee
WWW: http://mahon.cwx.net/
```

![](img/be7f02611e5cefde1a18c788fede22f7_298_1.png)

Figure 10-17. Easy Editor.

### Elvis

Elvis is a modern implementation of Vi that comes with many new features and extensions.

```
DEB: elvis
RPM: elvis
WWW: http://elvis.vi-editor.org/
```

![](img/be7f02611e5cefde1a18c788fede22f7_299_0.png)

Figure 10-18. Elvis.

### Emacs

Emacs is one of the two most popular text editors. A section all about it is located earlier in this chapter (see Recipe 10.1 [Using Emacs], page 232).

```
DEB: emacs-en-common
emacs21
RPM: emacs
WWW: http://www.emacs.org/
```

![](img/be7f02611e5cefde1a18c788fede22f7_299_1.png)

Figure 10-19. Emacs.

### Glimmer

Intended for use with computer programming languages, it has many features that appeal to programmers.

```
DEB: glimmer
RPM: glimmer
WWW: http://glimmer.sourceforge.net/
```

![](img/be7f02611e5cefde1a18c788fede22f7_300_0.png)

### JED

John E. Davis's editor offers many of the conveniences of Emacs and is geared specifically toward programmers. Features unique to it include drop-down menus that work in terminals; JED loads quickly, and makes editing files at a shell prompt easy and fast.

```
DEB: jed
RPM: jed
WWW: http://www.jedsoft.org/jed/
```

![](img/be7f02611e5cefde1a18c788fede22f7_300_1.png)

### JOE

Joe's Own Editor, joe, is a full-screen editor with a look and feel reminiscent of the old DOS text editors, such as EDIT.

```
DEB: joe
RPM: joe
WWW: http://sourceforge.net/projects/joe-editor/
```

![](img/be7f02611e5cefde1a18c788fede22f7_301_0.png)

Figure 10-22. Joe's Own Editor.

### Le

A multi-lingual editor for use in a terminal, with support for operating on rectangular blocks of text.

```
DEB: le
RPM: le
WWW: http://tinyurl.com/23325
```

![](img/be7f02611e5cefde1a18c788fede22f7_301_1.png)

Figure 10-23. Le.
