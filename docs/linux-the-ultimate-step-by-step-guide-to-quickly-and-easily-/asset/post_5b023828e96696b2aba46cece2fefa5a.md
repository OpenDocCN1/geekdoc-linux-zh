
some sensible options. The default prompt looks like:

```
Manual_page_name(sec) line x
```

where name denotes the manual page name, sec denotes the section it was found under and x the current line number. This is achieved by using the $LESS environment variable.

Supplying -r with a string will override this default. The string may contain the text $MAN_PN which will be expanded to the name of the current manual page and its section name surrounded by $(“” and “)”). The string used to produce the default could be expressed as:

```
Manual\ page\ $MAN_PN ?
ltline\ $t?L/$L:
byte\ $bB?s/s..? (END):?pB\ $pB\..
(press h for help or q to quit)
```

It is broken into three lines here for the sake of readability only. For its meaning see the man page for less.

The shell first evaluates the prompt string. All double quotes, back-quotes and backslashes in the prompt must be escaped by a preceding backslash. The prompt string may end in an escaped $ which may be followed by further options for less. By default, man sets the -ix8 options.

If you want to override man’s prompt string processing completely, use the $MANLESS environment variable described below.

## -7, --ascii

When viewing a pure ASCII manual page on a 7-bit terminal or terminal emulator, some characters may not display correctly when using the latin1 device description with GNU nroff. This option allows pure ASCII man pages to be displayed in ASCII with the latin1 device. It will not translate any latin1 text. The following table shows the translations performed: some parts of it may only be displayed properly when using GNU nroff's latin1 device. This option is ignored when using options -t, -H, -T, or -Z and may be useless for versions of nroff other than GNU's.

## -E encoding, --encoding=encoding
Generate output for a character encoding other than the default. For backward compatibility, encoding may be an nroff device such as ascii, latin1, or utf8 as well as a true character encoding such as UTF-8.

## --no-hyphenation, --nh
Normally, nroff will automatically hyphenate text at line breaks even in words that do not contain hyphens, if it is necessary to do lay out three words on a line without excessive spacing. This option disables automatic hyphenation, so words will only be hyphenated if they already contain hyphens. If you are writing a man page and simply want to prevent nroff from hyphenating a word at an inappropriate point, do not use this option, but consult the nroff documentation instead; for instance, you can put "\%" inside a word to indicate that it may be hyphenated at that point, or put "\%" at the start of a word to prevent it from being hyphenated.

## --no-justification, --nj
Normally, nroff will automatically justify text to both margins. This option disables full justification, leaving justified only to the left margin, sometimes called “ragged-right” text.

If you are writing a man page and simply want to prevent nroff from justifying certain paragraphs, do not use this option, but consult the nroff documentation; for instance, you can use the “.na”, “.nf”, “.fi”, and “.ad” requests to temporarily disable adjusting and filling.

## -p string, --preprocessor=string
Specify the sequence of preprocessors to run before nroff or troff/groff. Not all installations will have a full set of preprocessors. Some of the preprocessors and the letters used to designate them are: eqn (e), grap (g), pic (p), tbl (t), vgrind (v), refer (r). This option overrides the SMANROFFSEQ environment variable. zsoelim is always run as the first preprocessor.

- `-t, --troff`: Use groff -mandoc to format the man page to standard output. This option is not required in conjunction with `-H`, `-T`, or `-Z`.
- `-T[device], --troff-device[=device]`: This option is used to change groff (or possibly troff's) output to be suitable for a device other than the default. It implies `-t`. Examples include dvi, latin1, ps, utf8, X75 and X100.
- `-H[browser], --html[=browser]`: This option will cause groff to produce HTML output, and will display the output in a web browser. The choice of browser is determined by the optional browser argument if one is provided, by the SBROWSER environment variable, or by a compile-time default if that is unset (usually lynx). This option implies `-t`, and will only work with GNU troff.
- `-X[dpi], --gxditview[=dpi]`: This option displays the output of groff in a graphical window using the gxditview program. The `dpi` (dots per inch) may be 75, 75-12, 100, or 100-12, defaulting to 75; the -12 variants use a 12-point base font. This option implies -T with the `X75`, `X75-12`, `X100`, or `X100-12` devices, respectively.
- `-Z, --ditroff`: groff will run troff and then use an appropriate post-processor to produce output suitable for the chosen device. If groff -mandoc is groff, this option is passed to groff and will suppress the use of a post-processor. It implies `-t`.

## Section Numbers

The section numbers of the manual are listed below. While reading documentation, if you see a command name followed by a number in parentheses, the number refers to one of these sections. For example, man is the documentation of man found in section number 1. Some commands may have documentation in more than one section, so the numbers after the command name may direct you to the correct section to find a specific type of information.

The section numbers, and the topics they cover, are as follows:

| section # | Topic |
| :--- | :--- |
| **1** | Executable programs or shell commands |
| **2** | System calls (functions provided by the kernel) |
| **3** | Library calls (functions within program libraries) |
| **4** | Special files (usually found in /dev) |
| **5** | File formats and conventions eg /etc/passwd |
| **6** | Games |
| **7** | Miscellaneous (including macro packages and conventions), e.g. man, groff |
| **8** | System administration commands (usually only for root) |
| **9** | Kernel routines [Non standard] |

## Exit Status

When it terminates, **man** will return one of the following exit status:

- **0** Returned upon successful program execution.
- **1** Returned if there was a usage, syntax, or configuration file error.
- **2** Returned if there was an operational error.
- **3** Returned if a child process returned a non-zero exit status.
- **16** Returned if one or more of the pages, files, or keywords searched for did not exist or was not matched.

## Environment

**man** makes use of the following environment variables:

| Variable | Description |
| :--- | :--- |
| `MANPATH` | If `$MANPATH` is set, its value is **used as the path to search for manual pages**. |
| `MANOFFOPT` | The contents of `$MANOFFOPT` are added to the command line every time **man** invokes the formatter (*nroff*, *troff*, or **groff**). |
| `MANOFFSEQ` | If `$MANOFFSEQ` is set, its value is used to determine the set of preprocessors to pass each manual page through. The default preprocessor list is system-dependent. |
| `MANSECT` | If `$MANSECT` is set, its value is a colon-delimited list of sections and it is used to determine which man sections to search and in what order. |
| `MANPAGER`, `PAGER` | If `$MANPAGER` or `$PAGER` is set ($MANPAGER is used in preference), its value is used as the name of the program used to display the man page. By default, `pager -s` is used. The value may be a simple command name or a command with arguments, and may use shell quoting (backslashes, single quotes, or double quotes). It may not use pipes to connect multiple commands; if you need that, use a wrapper script, which may take the file to display either as an argument or on **standard input**. |
| `MANLESS` | If `$MANLESS` is set, man will not perform any of its usual processing to set up a prompt string for the `less` pager. Instead, the value of `$MANLESS` will be copied verbatim into `$LESS`. For example, if you want to set the prompt string unconditionally to “my prompt string”, set `$MANLESS` to ‘-Psmy prompt string’. |
