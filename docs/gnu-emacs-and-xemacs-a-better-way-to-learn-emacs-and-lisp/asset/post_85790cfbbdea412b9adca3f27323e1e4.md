
If it turns out that Mule is not a part of your Emacs installation and you need the capabilities it offers, you have two options. You have to either install a distribution package of the Mule version of Emacs or compile it from source.

In order to use Mule-enabled GNU Emacs built from source, you need to install the Leim distribution, which is available on this book’s CD-ROM in the same directory as the Emacs source: `/cdrom/emacs/source`. The GNU Emacs configure script needs no additional switches for Mule support, which is the default.

The XEmacs configure script does need a command-line switch to enable Mule:

```
./configure --with-mule
```

Consult the INSTALL file in the XEmacs source directory for further Mule-related configuration options.

The XEmacs Mule-based package is necessary. Depending on which language environments you need, you might also need the Egg-its (Japanese) and Leim (non-English and non-Japanese languages) packages.

## Fonts

Now that you have a Mule-enabled Emacs, you probably need to install additional X Window fonts. Emacs provides a handy sample file called HELLO, shown in Figure D.1, which includes a line of text for every language currently supported.

![](img/c8827ea52a0796def3f6891892ed9d3a_524_0.png)

Figure D.1 The HELLO File

Loading this file gives you quick evidence of missing fonts. Press `C-h` and type `H` to load the file. Any missing fonts appear as empty boxes. In XEmacs, tildes are used.

Unless you are impressively multilingual, there is no reason to install the available X fonts for each of these languages. Your Linux distribution CD-ROMs contain installable international font packages. The package file-names should give you an idea of which language's fonts are in which file.

## Input Methods and Language Environments

An input method is a set of instructions that tells Emacs how to interpret your keystrokes. The simplest input method is to simply interpret each character key as it appears on the keyboard. Typing an `a` causes a lowercase `a` to appear in the buffer, and so on. Variations of the basic English input method are used for European languages and some other languages that use characters such as umlauts and accented letters. In these methods, two keystrokes are necessary for the needed characters.

An additional layer of interpretation is needed for languages with different alphabets, such as Greek and Russian. When you use these input methods, the keyboard letters are mapped one-to-one to characters in the other alphabets.

Input methods become complicated for nonalphabetic languages such as Chinese and Thai. The number of characters tends to be in the thousands rather than the dozens. This means that several keystrokes are needed to type a character. You can view a descriptive list of all the available Emacs input methods by pressing `M-x` and typing:

```
list-input-methods
```

A language environment is a collection of settings that includes a default input method and coding system.

![](img/c8827ea52a0796def3f6891892ed9d3a_525_0.png)

> A coding system is a system for encoding written characters into a form usable by digital computers. ASCII, for example, is a coding system that uses a unique sequence of 7 bits for each character. Emacs automatically translates text written in any coding system into an internal system when reading data and translates it back into the original system when writing a file.

When multibyte characters are enabled, Emacs can display text written in any supported language if the correct fonts are available. Setting the language environment changes the default coding system and the input method to appropriate settings for the selected language.

If you would like to read a short description of a particular language environment, press `C-h`, type `L`, and press `Tab`.

The `Tab` key summons a Completions window with a list of all the supported language environments. Choose one, type the name into the minibuffer, and press `Enter`.

You can change the language environment for the current Emacs session by pressing `M-x` and typing `set-language-environment`.

You are prompted for a name. If you aren't sure of the name or spelling, press `Tab`, and a Completions window appears.

You can also change this setting by selecting one of the items on the “Set language environment” submenu of the Mule menu.

GNU Emacs lets you permanently change your language environment with Customize. Press `M-x` and type `customize-option`.

When prompted in the minibuffer, type `customize-language-environment`.

When the Customize buffer appears, type the environment you want as the default into the text entry field, and then select Save for Future Sessions from the State pop-up menu.

## The Mule Project

In 1987, a group of Japanese Emacs users developed a Japanese version of Emacs called Nemacs. Once they had the new version working well with their language, these developers contacted the Free Software Foundation and offered the code as a possible addition to Emacs. The FSF demurred. Although the prospect of making Emacs available to a new community of users was tempting, the FSF thought that a more general approach that could support any language would be preferable.

This situation provided the impetus for a new project, the Multilingual Enhancement, or Mule. The Japanese developers began with the Japanese-language code used in the Nemacs editor and generalized it so that new languages could be supported. The result was an Emacs extension rather than a separate editor. Over the next few years, new languages were added as contributors from various language backgrounds joined the project. During this period, Mule was an external Emacs extension. In 1997, Mule was accepted as an integral part of GNU Emacs. The XEmacs team opted for making Mule an optional, although official, package.

![](img/c8827ea52a0796def3f6891892ed9d3a_528_0.png)

### associated list (alist)

An Emacs Lisp term for a special type of list in which each element is a keyword-value pair. See Chapter 7 for examples of how this type of list is used in an Emacs Lisp file.

### atom

A basic unit of a Lisp expression. An atom can be a numeral, a symbol (which may identify a function or variable), or a quoted string. See *symbol*.

### auto-save

Emacs periodically saves a copy of a buffer as you edit it to a file that is deleted after the buffer is successfully saved to disk. This temporary file is updated if either Emacs or the system crashes. The auto-save file can be recovered later, minimizing your chances of losing work. See Chapter 22 for more details.

### bookmark

A location within a buffer saved to a bookmark file, allowing you to return easily. Normally, opening a file results in the cursor's being placed at the beginning of the new buffer. Selecting a bookmark is a way to load a file with the cursor placed at a saved spot.

### buffer

A copy of a file that is visible in an Emacs window. When changes are made and the buffer is saved, the contents of the buffer overwrite the original file. Emacs also creates temporary buffers that don't correspond to an actual file, such as the `*Scratch*` buffer.

### byte-compile

An Emacs Lisp file can be subjected to a process called byte compilation, which makes the file quicker and easier to load. The file becomes unreadable by humans, because some of the Lisp code is turned into byte-code, a compact form of code that is easily processed by the Emacs Lisp interpreter. A byte-compiled file can be identified by the letter “c” appended to the file's name. For example, `code.el` becomes `code.elc`.

### car

An Emacs Lisp term meaning the first element in a list. See also *cdr*.

### cdr

All the elements of an Emacs Lisp list except the first. What remains of a list when the list's *car* is removed. See also *car*.

### comment

A human-readable section of a source code file that is tagged with special characters that force the interpreter or compiler to ignore the section. Text-formatting languages also have special commenting characters. When marked up, text is processed and the commented sections are skipped.

### completion

Emacs can finish typing incomplete file names, commands, or names of variables. You just type a partial name and press `Tab`, and the remainder of the name is completed.

### cons

In Emacs Lisp, to *cons* an element to a list is to add it to the front of the list. *Cons* is a built-in function.
