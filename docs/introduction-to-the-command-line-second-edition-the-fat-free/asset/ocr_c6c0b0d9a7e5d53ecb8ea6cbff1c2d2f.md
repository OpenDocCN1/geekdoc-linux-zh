# strings

**Purpose:** Extract readable characters from binary files.

**Usage syntax:** `strings [OPTIONS] [FILE]`

```
$ strings unknown.mp3
...
T'AG Girl You Know It's True
Milli Vanilli
Girl You Know It's True
1989
...
```

Using the strings command to extract text from a binary file

The `strings` command extracts text from binary files. Binary files contain data that is unreadable using standard text processing programs. Examples of binary files include MP3, JPEG, and MPEG to name a few.

In the above example, readable text is extracted from the `unknown.mp3` file. This information can be used to identify the contents of the binary file.

> Note The `strings` command displays results that are a minimum of 4 characters by default. You can override the default minimum character length using the `‑n` option.

Common usage examples:

+   `strings [FILE]` - Display readable text characters in a binary file
+   `strings -n [NUM] [FILE]` - Set the minimum number of characters