
![](img/8bf3d083d04b4cc3d79bd39657ac711a_162_0.png)

The large area with the word `beginning` in it is where the text is being streamed. The text in the lower-left window is a shrunken view of the entire file, the text in the lower-right window is the paragraph from which the current word comes from.

To open another file, choose it from the menu; you can have many files open in sview at once. sview places each file in its own buffer. You can also paste the X selection into a buffer of its own—to switch to a different buffer, choose its name from the Buffer menu.

Type Q to quit reading and exit sview.

The following table lists the keyboard commands used in sview and describes their meaning.

| KEYSTROKE | DESCRIPTION |
|---|---|
| @leftarrow | Decrease the stream speed. [GNU INFO BUG: any <> in the preceding line should be the <- arrow key.] |
| @rightarrow | Increase the stream speed. [GNU INFO BUG: any <> in the preceding line should be the -> arrow key.] |
| C-o | Open a file. |
| C-q | Quit viewing text and exit sview. |
| C-w | Erase the current text buffer. |
| M-n | Move forward to the next word. |
| M-p | Move backward to the previous word. |
| S | Toggle the streaming of text. |

## 10.4 Viewing a Character Chart

To view a character chart containing a list of all the valid characters in the ASCII character set and the character codes to use to type them, view the asciiman page.

- To view an ASCII character set, type:

```
$ man ascii RET
```

You can use the octal codes listed for each character to type them in Emacs---see Inserting Special Characters in Emacs.

The default Linux character set, the ISO 8859-1 ("Latin 1") character set, contains all of the standard ASCII character set plus an additional 128 characters.

To view the ISO 8859-1 character set, which contains an extended set of characters above the standard 127 ASCII characters, view the iso_8859_1man page.

- To view the ISO 8859-1 character set, type:

```
$ man iso_8859_1 RET
```

You can use this page to see all of the characters in this character set and how to input them.

NOTE: There's a special way to "quote" these characters in Emacs; this technique is described in Inserting Special Characters in Emacs.

The `miscfiles' package also contains charts for these character sets, as explained in Word Lists and Reference Files.

## 11. Text Editing

Text editing is one of the most fundamental activities of computing on Linux-based systems, or most any computer for that matter. We edit text when writing a document, sending email, making a Web page, posting an article for Usenet, programming—and the list goes on. Most people spend a good deal of their computing time editing text with a text editor application.

There are a lot of text editors to choose from on Linux systems, as the first recipe in this chapter shows, but the majority of editors fit in one of two families of editor: Emacs and Vi. Most users prefer one or the other; rarely is one adept at both. I give more coverage to Emacs, and not only because it's my preferred editor—its keystroke commands are used by default in many other tools and applications, including the bash shell (see section The Shell).

- 11.1 Choosing the Perfect Text Editor
- Overview of text editors.
- 11.2 Emacs
- Introducing the Emacs editor.
- 11.3 Running a Vi Tutorial
- Learning to use the Vi editor.
- 11.4 Selecting Text
- Selecting text.
- 11.5 Editing Streams of Text
- Editing a stream of text in batch.
- 11.6 Concatenating Text
- Concatenating text.
- 11.7 Including Text Files
- Including text files into new files.

### 11.1 Choosing the Perfect Text Editor

The following table describes some of the more interesting text editors available, and includes information about their special traits and characteristics.

| TEXT EDITOR | DESCRIPTION |
|---|---|
| ae | Anthony's Editor, ae, is a simple, easy-to-use text editor. It has modes to emulate the behavior of other text editors. {@sf{Debian}}: `ae` {@sf{WWW}}: http://dmz.org/Computers/Software/Editors/Vi/ |
| cooledit | Cooledit is a popular, fast text editor for use in X; its features include anti-aliased fonts, Unicode support, and extensibility via the Python programming language. {@sf{Debian}}: `cooledit` {@sf{WWW}}: http://cooledit.sourceforge.net/ |
| dedit | DEdit is a simple editor for use in X with GNOME installed. It can read compressed files and display Japanese characters. {@sf{Debian}}: `dedit` |
| ee | Intended to be an editor that novices can begin using immediately, the Easy Editor features pop-up menus. {@sf{Debian}}: `ee` {@sf{WWW}}: http://mahon.cwx.net/ |
