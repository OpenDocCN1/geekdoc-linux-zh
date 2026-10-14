There are a few methods for viewing text containing backspace underlines in different ways.

# METHOD #1

Use less to peruse text containing backspace underlines (see Recipe 9.1 [Perusing Text], page 211).

⇒ To peruse the file term-paper so that you can view any backspace underlines it contains, type:

```
$ less term-paper [RET]
```

# METHOD #2

Use the ul tool to output text containing backspace underlines, so that these underlines are displayed correctly on your terminal.

⇒ To output the file term-paper so that you can view underlined text, type:

```
$ ul term-paper [RET]
```

This command converts any backspace underlines in term-paper to character sequences that your terminal can display; thus, if you have cat or some other command further on a pipeline, the text will be displayed properly on your screen.

⇒ To output the file term-paper with cat, showing any underlined text on your terminal, type:

```
$ ul term-paper | cat [RET]
```

# METHOD #3

Use colcrt to convert backspace underlining to dashing (a row of hyphen characters, like "-------") drawn beneath the underlined text.

⇒ To output the file term-paper, with all backspace underlining converted to dashing, type:

```
$ colcrt term-paper [RET]
```

Dashing inserts a new line in the text directly underneath any underlined text, and this is not always desirable. Use the "-" option to supress underlining entirely, and display any underlined text as plain text.

⇒ To output the file term-paper, with all backspace underlining removed, type:

```
$ colcrt - term-paper [RET]
```