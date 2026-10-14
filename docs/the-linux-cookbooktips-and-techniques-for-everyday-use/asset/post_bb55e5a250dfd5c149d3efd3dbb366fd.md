
elvis Elvis is a modern implementation of Vi that comes with many new features and extensions. {@sf{Debian}: `elvis`} {@sf{WWW}: http://elvis-vi-editor.org}

emacs Emacs is one of the two most-popular text editors. I've devoted an entire section to it in this book: Emacs. {@sf{Debian}: `emacs-common`} {@sf{Debian}: `emacs20`} {@sf{WWW}: `http://www.emacs.org/`}

jed John E. Davis's jed offers many of the conveniences of Emacs and is geared specifically toward programmers. Features unique to it include drop-down menus that work in the console; jed loads quickly, and makes editing files at a shell prompt easy and fast. {@sf{Debian}: `jed`} {@sf{WWW}: http://space.mit.edu/~davis/jed.html}

joe Joe's Own Editor, joe, is a full-screen editor with a look and feel reminiscent of old DOS text editors like EDIT. {@sf{Debian}: `joe`} {@sf{WWW}: ftp://ftp.std.com/src/editors/}

nano Nano is a free software editor inspired by Pico, the editor that is included with the University of Washington's proprietary Pine email program. It's also faster than Pico, and comes with more features. {@sf{Debian}: `nano`} {@sf{WWW}: http://www.nano-editor.org/}

ted Ted is a WYSIWYG text editor for use in X which reads and writes `.rtf` files in Microsoft's "Rich Text Format." {@sf{Debian}: `ted`} {@sf{WWW}: http://www.nllgg.nl/Ted/}

the The Hesselink Editor is a configurable editor that uses the Rexx macro language. It was inspired by the XEDIT editor for VM/CMS and the Kedit editor for DOS. {@sf{Debian}: `the`} {@sf{Debian}: `the-doc`} {@sf{WWW}: http://www.lightlink.com/hessling/THE/}

vi Vi (pronounced "vee," or sometimes "vee-eye") is a visual, or full-screen, editor. Touch typists often find its keystroke commands enable very fast editing. Together with Emacs, Vi shares the spotlight for most popular editor on Linux and Unix-based systems in general. Both were initially written in the same period, and both have their staunch adherents. To run a hands-on tutorial, see Running a Vi Tutorial. {@sf{Debian}: `nvi`} {@sf{WWW}: ftp://mongoose.bostic.com/pub/nvi.tar.gz}

vim Like the Elvis editor, Vim ("Vi improved") is a modern implementation of Vi whose new features include syntax coloring, scrollbars and menus, mouse support, and built-in help. {@sf{Debian}: `vim`} {@sf{WWW}: http://www.vim.org/}

wily Wily, an interesting mouse-centric editor, is inspired by the Acme editor from AT&T's Plan 9 experimental operating system. Wily commands consist of various combinations of the three mouse buttons, called chords, which can be tricky to master. {@sf{Debian}: `wily`} {@sf{WWW}: http://www.cs.su.oz.au/~gary/wily/}

xedit Xedit is a simple text editor that comes with, and works in, X. It lets you insert, delete, copy and paste text as well as open and save files---the very basics. {@sf{Debian}: `xcontrib`}

xemacs XEmacs is a version of Emacs with advanced capabilities for use in X, including the ability to display images. {@sf{Debian}: `emacs-common`} {@sf{Debian}: `xemacs`} {@sf{WWW}: http://www.xemacs.org/}

## 11.2 Emacs

```
@sf(Debian): 'emacs-common'
@sf(WWW): 'http://www.emacs.org/'
```

To call Emacs a text editor does not do it justice—it’s a large application capable of performing many functions, including reading email and Usenet news, browsing the World Wide Web, and even perfunctory psychoanalysis.

There is more than one version of Emacs. GNU Emacs is the Emacs released under the auspices of Richard Stallman, who wrote the original Emacs predecessor in the 1970s. XEmacs (formerly Lucid Emacs) offers essentially the same features GNU Emacs does, but also contains its own features for use with the X Window System (it also behaves differently from GNU Emacs in some minor ways).

GNU Emacs and XEmacs are by far the most popular emacsen (as they are referred to in number); other flavors include jed (described in the previous section) and Chet’s Emacs, ce, developed by a programmer at Case Western Reserve University.

Following is a brief introduction to using Emacs, interspersed with the necessary Emacs jargon; following that are recipes that describe how to use some of Emacs’s advanced editing features.

- 11.2.1 Getting Acquainted with Emacs
- How to learn Emacs.
- 11.2.2 Basic Emacs Editing Keys
- The basic Emacs editing keys.
- 11.2.3 Making Abbreviations in Emacs
- Making abbreviations to save time.
- 11.2.4 Recording and Running Macros in Emacs
- Making macros to save time.
- 11.2.5 Inserting Special Characters in Emacs
- Inserting special characters in Emacs.

### 11.2.1 Getting Acquainted with Emacs

Start Emacs in the usual way, either by choosing it from the menu supplied by your window manager in X, or by typing its name (in lowercase letters) at a shell prompt.

- To start GNU Emacs at a shell prompt, type:

```
$ emacs RET
```

- To start XEmacs at a shell prompt, type:
