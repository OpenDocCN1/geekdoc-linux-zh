# 11.2 Emacs

```
@sf(Debian): 'emacs-common'
@sf(WWW): 'http://www.emacs.org/'
```

To call Emacs a text editor does not do it justice—it’s a large application capable of performing many functions, including reading email and Usenet news, browsing the World Wide Web, and even perfunctory psychoanalysis.

There is more than one version of Emacs. GNU Emacs is the Emacs released under the auspices of Richard Stallman, who wrote the original Emacs predecessor in the 1970s. XEmacs (formerly Lucid Emacs) offers essentially the same features GNU Emacs does, but also contains its own features for use with the X Window System (it also behaves differently from GNU Emacs in some minor ways).

GNU Emacs and XEmacs are by far the most popular emacsen (as they are referred to in number); other flavors include jed (described in the previous section) and Chet’s Emacs, ce, developed by a programmer at Case Western Reserve University.

Following is a brief introduction to using Emacs, interspersed with the necessary Emacs jargon; following that are recipes that describe how to use some of Emacs’s advanced editing features.

+   11.2.1 Getting Acquainted with Emacs
+   How to learn Emacs.
+   11.2.2 Basic Emacs Editing Keys
+   The basic Emacs editing keys.
+   11.2.3 Making Abbreviations in Emacs
+   Making abbreviations to save time.
+   11.2.4 Recording and Running Macros in Emacs
+   Making macros to save time.
+   11.2.5 Inserting Special Characters in Emacs
+   Inserting special characters in Emacs.

# 11.2.1 Getting Acquainted with Emacs

Start Emacs in the usual way, either by choosing it from the menu supplied by your window manager in X, or by typing its name (in lowercase letters) at a shell prompt.

+   To start GNU Emacs at a shell prompt, type:

```
$ emacs RET
```

+   To start XEmacs at a shell prompt, type: