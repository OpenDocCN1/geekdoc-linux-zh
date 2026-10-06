# Case Conversion

Sometimes, we need to change text from upper to lower case and vice versa, vim has the following case conversion commands:

| Toggle the case of the current character |
| gU | Convert text to upper case |
| gu | Convert text to lower case |

Both the gU and gu commands can be applied to selected text in visual mode or used in conjunction with motion commands or text selections. For example:

```
guis   Convert the current sentence to upper case
guf:   Convert text from the cursor position to the next ':'
       character on the current line
```

# File Format Conversion

Once a while, we are afflicted with a text file that was created or used in a DOS/Windows system. These files will contain an extra carriage return at the end of each line. Vim will indicate this after loading the file by displaying a "DOS" message at the bottom of the editing window. To correct this annoying condition, do the following:

```
:set fileformat=unix
```

The file will be rewritten in the correct format.

Help topics: 'textwidth' gq 'fileformat' ~ gu gU

# Macros

Text editing sometimes means we get stuck with a tedious repetitive editing task where we do the same set of operations over and again again. This is the bane of every computer user. Fortunately, vim provides us a way to record a sequence of operations we can later playback as. These recordings are called macros.

To create a macro, we begin recording typing q followed by a single letter. The character typed after q becomes the name of the macro. After start recording, everything we gets gets in the macro. To conclude, we type q again.

To demonstrate, let's consider our block comment. To create a macro that will remove a character symbol from the beginning of the line, we would do this: move to the first line in the comment block and type the following command:

Let's break down what this sequence:

| qa | Start recording macro "a" |
| ^ | Move to the first non-whitespace character in the current line |
| xx | Delete the first two characters under the cursor |
| j | Move down one line |

172 Vim, with Vitor