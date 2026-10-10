
the original window in the new window. After you move into the new window, you can use the c-x c-f command to load a new file or use one of the commands to switch to a different buffer area in the new window.

To close a window, move to it and use the c-x 0 (that's a zero) command. If you want to close all the windows except the one you're in, use the c-x 1 (that's a numerical one) command.

## Using Emacs in a GUI

If you use Emacs from a GUI environment (such as in the GNOME Shell desktop), it starts in graphical mode, as shown in Figure 10–5.

![](img/a5025f22e05b92f409563a958cac7312_351_0.png)

FIGURE 10–5 The Emacs graphical window

If you've already used Emacs in console mode, you should be fairly familiar with the graphical mode. All the key commands are available as menu bar items. The Emacs menu bar contains the following items:

- **File** allows you to open files in the window, create new windows, close windows, save buffers, and print buffers.
- **Edit** allows you to cut and copy selected text to the clipboard, paste clipboard data to the current cursor position, search for text, and replace text.
- **Options** provides settings for many more Emacs features, such as highlighting, word wrap, cursor type, and setting fonts.
- **Buffers** lists the current buffers available and allows you to easily switch between buffer areas.
- **Tools** provides access to the advanced features in Emacs, such as the command-line interface access, spell checking, comparing text between files (called diff), sending an email message, calendar, and the calculator.
- **C** allows advanced settings for highlighting C program syntax, compiling, running, and debugging the code.
- **Help** provides the Emacs manual online for access to help on specific Emacs functions.

The graphical Emacs window is an example of an older console application that made the migration to the graphical world. Now that many Linux distributions provide graphical desktops (even on servers that don't need them), graphical editors are becoming more commonplace. Popular Linux desktop environments (such as KDE Plasma and GNOME Shell) have also provided graphical text editors specifically for their environments, which are covered in the rest of this chapter.

## Exploring the KDE Family of Editors

If you're using a Linux distribution that uses the KDE Plasma desktop environment, you have a couple of options when it comes to text editors. The KDE project officially supports two popular text editors:

- **KWrite:** A single-screen text-editing package
- **Kate**: A full-featured, multiwindow text-editing package

Both of these editors are graphical text editors that contain many advanced features. The Kate editor also provides extra niceties not often found in standard text editors. This section describes each of the editors and shows some of the features you can use to help with your shell script editing.

## Looking at the KWrite editor

The basic editor for the KDE Plasma environment is KWrite. It provides simple word processing--style text editing, along with support for code syntax highlighting and editing. The default KWrite editing window is shown in Figure 10-6.

![](img/a5025f22e05b92f409563a958cac7312_353_0.png)

FIGURE 10-6 The default KWrite window editing a shell script program

You can't tell from Figure 10-6, but the KWrite editor recognizes several types of programming languages and uses color coding to distinguish constants, functions, and comments. The KWrite editing window provides full cut and paste capabilities, using the mouse and the arrow keys. As with a word processor, you can highlight and cut (or copy) text anywhere in the buffer area and paste it at any other place.

> **TIP**
> Typically, KWrite is no longer installed by default on the KDE desktop environment. However, you can easily install it (see Chapter 9) on Plasma or other desktop environments, where available. The package name is `kwrite`.

To edit a file using KWrite, you can either select KWrite from the KDE menu system on your desktop (some Linux distributions even create a Panel icon for it) or start it from the command-line prompt:

```
$ kwrite factorial.sh
```

The `kwrite` command has several command-line parameters you can use to customize how it starts. Here are few of the more practical ones:

- `--stdin` causes KWrite to read data from the standard input device instead of a file.
- `--encoding` specifies a character encoding type to use for the file.
- `--line` specifies a line number in the file to start at in the editor window.
- `--column` specifies a column number in the file to start at in the editor window.

The KWrite editor provides both a menu bar and a toolbar at the top of the edit window, allowing you to select features and change the configuration settings of the KWrite editor.

The menu bar contains these items:

- **File** loads, saves, prints, and exports text from files.
- **Edit** manipulates text in the buffer area.
- **View** manages how the text appears in the editor window.
- **Bookmarks** handle pointers to return to specific locations in the text; this option may need to be enabled in the configurations.
- **Tools** contains specialized features to manipulate the text.
- **Settings** configures the way the editor handles text.
- **Help** gives you information about the editor and commands.

The Edit menu bar item provides commands for all your text-editing needs. Instead of having to remember cryptic key commands (which by the way, KWrite also supports), you can just select items in the Edit menu bar, as shown in Table 10-3.

### TABLE 10-3 The KWrite Edit Menu Items

| Item | Description |
| :--- | :--- |
| Undo | Reverses the last action or operation. |
| Redo | Reverses the last undo action. |
| Cut | Deletes the selected text and places it in the clipboard. |
| Copy | Copies the selected text to the clipboard. |
| Paste | Inserts the current contents of the clipboard at the current cursor position. |
| Clipboard History | Displays portions of text recently copied to the clipboard from which you can select to paste. |
| Copy As HTML | Copies the selected text as HTML. |
| Select All | Selects all text in the editor. |
| Deselect | Deselects any text that is currently selected. |
| Block Selection | Toggles on/off block selection mode which allows vertical text selection. |
| Mode | |
| Input Modes | Toggles between a normal and a vi-like editing mode. |
| Overwrite Mode | Toggles insert mode to overwrite mode, replacing text with new typed text instead of just inserting the new text. |
| Find | Produces the Find Text dialog box, which allows you to customize a text search. |
| Find Variants | Provides a submenu of various text searches — Find Next, Find Previous, Find Selected, and Find Selected Backwards. |
| Replace | Produces the Replace With dialog box, which allows you to customize a text search and replace. |
| Go To | Provides a submenu of various Go To choices — Move To Matching Bracket, Select To Matching Bracket, Move To Previous Modified Line, Move To Next Modified Line, Go To Line. |

The Find feature has two modes. Normal mode performs simple text searches and power searches. Replace mode lets you do advanced searching and replacing if necessary. You toggle between the two modes using the icon on the lower-right side of the window, as shown in Figure 10-7.

![](img/a5025f22e05b92f409563a958cac7312_357_0.png)

**FIGURE 10-7** The KWrite Find section

The Find power mode allows you to search not only with words, but with a regular expression (discussed in **Chapter 20**, “Regular Expressions”) for the search. You can use some other options to customize the search as well, indicating, for example, whether or not to perform a case-sensitive search or to look only for whole words instead of finding the text within words.

The **Tools** menu bar item provides several handy features for working with the text in the buffer area. **Table 10-4** describes the tools available in KWrite.

### TABLE 10-4 The KWrite Tools

| Tool | Description |
| :--- | :--- |
| Read Only | Locks the text so that no changes can be made while in |
