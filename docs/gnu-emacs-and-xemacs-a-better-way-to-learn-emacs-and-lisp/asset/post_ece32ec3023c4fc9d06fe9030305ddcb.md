
## Formatting Commands

When you are writing text such as an e-mail, an article, a chapter of a book, or anything intended to be read by you or other people, you don't want to have to wrap lines manually. By default, Emacs doesn't automatically wrap lines, but it does a sort of pseudo-wrapping so that lines don't extend beyond the screen. This is indicated by a backslash (in GNU Emacs) or an arrow (in XEmacs). Lines are broken in the middle of a word if necessary. Most Emacs users configure the editor to automatically fill paragraphs (wrap long lines to a specific width) when in text mode or when in any modes derived from text mode (such as message mode, used when you write e-mail).

### Auto-Fill Mode

Customization of Emacs is fully dealt with in Chapter 4, which shows you how to use Customize to write entries in your `.emacs` file automatically, and Chapter 9, which teaches you how to write your own `.emacs` file. But this word-wrap issue is important enough (for usability reasons) to justify jumping ahead a bit.

Emacs comes with a text-filling minor mode (a mode that coexists with and supplements a major mode) called auto-fill mode. You can easily set an option that sets that mode to be the default when no other mode is specified. This means that whenever a new file is opened, it is in auto-fill mode, and your text will wrap. Here are step-by-step instructions:

- 1. Start Emacs and create a new, empty `.emacs` file by pressing Ctrl-x Ctrl-f.
- 2. You are prompted in the minibuffer for a file name. Type `~/.emacs`. The screen will be empty unless you already have an `.emacs` file. Type in these two Lisp expressions:

```
(setq default-major-mode 'text-mode)
(add-hook 'text-mode-hook 'turn-on-auto-fill)
```

Make sure you include all the parentheses, and don't forget the single quote just before the words *turn* and *text*.

- 3. Check to make sure that you typed these lines correctly by moving the cursor to the end of the first line and pressing Ctrl-x Ctrl-c. This command tells Emacs to evaluate the Lisp expression. If it’s invalid, an error message appears.
- 4. Move the cursor to the end of the second line and press Ctrl-x Ctrl-c again. If there are no errors, text mode with auto-fill turned on will be active for the remainder of the Emacs session.
- 5. Save the file by pressing Ctrl-x Ctrl-s. The new setting will be in effect for future Emacs sessions.

### The Fill-Column Variable

Emacs comes with the text width for auto-fill mode set at 70 columns, a reasonable default for average computer screens and Emacs window sizes. If 70 columns is too wide or too narrow for your screen, the fill-column variable can be changed. Press Ctrl-u, type `number`, and press Ctrl-x f.

Substitute any desired number of columns for `number` in the command. See Chapter 9 for ways to make changes such as this one permanent.

### Capitalization and Lowercase

Changing capitalized words to uncapitalized and vice versa is a common editing task. It’s easy to forget to capitalize a proper name or the first word of a sentence. A tedious way to correct such typos is to move the cursor back to the offending character, delete it, and then type the proper character. That’s quite a few steps for a trivial but commonplace operation.

Emacs has several built-in commands for dealing with such situations. These commands are quick to type and will quickly become second nature to you:

- M-c Capitalizes a word.
- M-l Converts a word to all-lowercase.
- M-u Converts a word to all-uppercase.

These commands don’t require you to carefully place the cursor on the first character; anywhere in the word is fine.

### Transposition

Another common error is transposed words or characters. You can quickly fix these annoying errors using these commands:

- Ctrl-t Transposes two letters.
- M-t Transposes two words.
- Ctrl-x Ctrl-t Transposes two lines.

### Windows, Frames, and Buffers

The terms window and frame have meanings in an Emacs context that differ from their conventional meanings. Usually a window in a GUI like X Windows is defined as a rectangular, movable, and resizable bordered box within which an application runs. In Emacs lingo, this is a frame, and a window is a subdivision of a frame that displays a single buffer.

### Multiple Windows

Normally, when you switch from one buffer to another, each one fills the entire frame (or the entire screen when Emacs is running on a non-X console). Sometimes it’s helpful to be able to see two or more buffers at once, or two or more sections of a single buffer at once, as shown in Figure 3.4.

![](img/c8827ea52a0796def3f6891892ed9d3a_92_0.png)

There are several keyboard commands for creating, destroying, and moving between windows:

- Ctrl-x 2 Splits the current full-size window into two shorter windows, one above the other.
- Ctrl-x 3 Splits the current window into two narrower side-by-side windows.
- Ctrl-x o Moves point to the next window or, if there are more than two, to the next window in a clockwise direction.
- Ctrl-x 1 Makes the current window full-size, deleting the other one (but not deleting the other window's buffer).
- Ctrl-x 0 Removes the current window, allowing the other window to expand to full size.
- Ctrl-x ^ Enlarges the current window while making the other window smaller.

### Frames

An Emacs frame is Emacs running in an X window, but Emacs can run in more than one frame without starting another Emacs session. These frames can be dealt with as with any X window: They can be resized, and any window manager command such as the keyboard commands for next window and previous window can be used normally. The Emacs commands for manipulating frames are analogous to the window commands in the preceding section:

- Ctrl-x 5 2 Creates a new frame with the same buffer visible as in the original.
- Ctrl-x 5 o Moves focus to another frame.
- Ctrl-x 5 0 Removes the currently-active frame.
- Ctrl-x 5 b Makes a new frame and displays the previous buffer in it.
- Ctrl-x 5 f Loads a new file in a new frame.

Although the concept of frames doesn't translate well to the Linux virtual console, with its individual full-screen windows, recent versions of XEmacs do provide switchable frames in console sessions. These could be thought of as separate window groups.

### Shell Commands

Emacs provides several ways to run external shell commands. It even allows you to devote a window to a complete interactive shell, just like your shell running in an xterm or in a virtual console.

#### Noninteractive Commands

M-! is a quick and simple key command that runs an external shell command and directs its output to an Emacs window called Shell Command Output. Figure 3.5 shows the output of the df command in its own new window. There are several advantages to running a command from within Emacs. You can treat the output just as you would any other text in a buffer. You can cut or copy it to another buffer, save it to file, or refer to it later in the session.

Another interesting feature is a variant of the M-! command. Use one of the standard Emacs methods of marking a region, and then press M-!. Emacs will prompt you for a shell command in the minibuffer.

As an example, Figure 3.6 shows the result of piping a selected region of text through the GNU pr text utility (used with the -a option, which doublespaces the output).

#### Inserting Command Output into a Buffer

Rather than copying text from the Shell Command Output buffer, you can run an external command and have the output appear at point in your current buffer. All you have to do is precede the basic shell command with Ctrl-u by pressing Ctrl-u M-!. This variation can also be used with the shell command on-region. The original region disappears and is replaced by the output of the shell command. Press Ctrl-u M-l.

![](img/c8827ea52a0796def3f6891892ed9d3a_94_0.png)

Figure 3.5 Shell Command Output
