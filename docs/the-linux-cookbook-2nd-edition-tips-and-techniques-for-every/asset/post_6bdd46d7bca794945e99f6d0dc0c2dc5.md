
## III. TEXT

## 9. Viewing Text

Dealing with textual matter is the meat of Linux (and of most computing), so there are going to be many chapters about the various aspects of text. This first chapter in this part of the book shows how to view text on your display screen.

Text files come in any number of formats, from formatted text in some particular language—such as English or the C programming language—to saved email messages or HTML files. Plain text files don’t have to have a .txt or .text file name extension, although they often do (see Appendix B [Conventional File Name Extensions], page 723).

If you are not sure whether the content of a file is text or not, use file to find out, as described in Recipe 8.1.1 [Determining a File’s Type and Format], page 187.

A tool that just allows you to view text on the screen, but not edit it, is called a pager. When most people view text without editing it, they use less, which is described in the following recipes.

There are many ways to view or otherwise output text. For example, you can view text as you browse files and their contents, as described in Recipe 5.10 [Browsing Files and Directories], page 157. When your intention is to edit the text of a file, you should open it in a text editor, as described in Chapter 10 [Editing Text], page 231. The Vi editor comes with a special command, view, to open a file in read-only mode with Vi, so that it can only be viewed—you cannot, accidentally or intentionally, make any changes to the file while it is open if you use this command.

Some kinds of files—such as PostScript, DVI, and PDF files—often contain text in them, but they are technically not text files. These are image format files, and I describe methods for viewing them in Recipe 17.4 [Previewing Print Files], page 413.

### 9.1 Perusing Text

Use less to peruse text, viewing it one screen (or “page”) at a time. The less tool works on either files or standard output—it is popularly used as the last command on a pipeline so that you can page through the text output of some commands. For an example, see Recipe 3.2.4 [Redirecting Output to Another Command’s Input], page 69. The following recipes describe various ways to use less.

Another tool, `zless`, is identical to `less`, but you use it to view compressed text files; it allows you to read a compressed text file’s contents without having to uncompress the file first (see Recipe 8.4 [Using File Compression], page 196). Most of the system documentation in the `/usr/doc` and `/usr/share/doc` directories, for example, consists of compressed text files.

You may, on occasion, be confronted with a reference to a command for paging text, called `more`. It was the standard tool for paging text until it gave way to `less` in the early to mid 1990s; `less` comes with many more options—its most notable advantage being the ability to scroll backward through a file—but at the expense of being almost exactly three times the size of `more`. Hence, there are two meanings to the saying, “less is more.”

The following table summarizes the most essential keyboard commands for paging through text in `less`. It lists the keystrokes and describes the commands.

| Keystroke | Description |
|---|---|
| `↑` | Scroll back through the text (“up”) one line. |
| `↓` | Scroll forward through the text (“down”) one line. |
| `←` or `→` | Scroll horizontally (left or right) one tab stop; useful for perusing files that contain long lines. |
| `PgUp` or `SPACEBAR` | Scroll backward (“up”) through the text by one screenful. |
| `PgDn` | Scroll forward (“down”) through the text by one screenful. |
| `←` | Move to the beginning of the file. |
| `→` | Move to the end of the file. |
| `/pattern` | Search forward through the file for lines containing *pattern*. |
| `?pattern` | Search backward through the file for lines containing *pattern*. |

### *Cursor Movement*

### *Searching Text*
