Use the special `--help-pretty-print` option to list the languages supported by the copy of ensript you have.

+   - To peruse a list of currently supported languages, type:

```
$ ensript --help-pretty-print | less RET
```

# 16.2.4 Outputting Text with Fancy Headers

To output text with fancy graphic headers, where the header text is set in blocks of various shades of gray, use ensript with the `-G` option.

+   - To print the contents of the text file `saved-mail` with fancy headers on a PostScript printer, type:

```
$ ensript -G saved-mail RET
```

+   - To make a PostScript file called `saved-mail.ps` containing the contents of the text file `saved-mail`, with fancy headers, type:

```
$ ensript -G -p saved-mail.ps saved-mail RET
```

Without the `-G` option, ensript outputs text with a plain header in bold text, printing the file name and the time it was last modified. The `-B` option, as described earlier, omits all headers.

You can customize the header text by quoting the text you want to use as an argument to the `-b` option. Use the special symbol ` $% ` to specify the current page number in the header text.

+   - To print the contents of the text file `saved-mail` with a custom header label containing the current page number, type:

```
$ ensript -b "Page $% of the saved email archive" saved-mail RET
```

*NOTE:* You can create your own custom fancy headers, too---this is described in the `CUSTOMIZATION` section of the ensriptman page.