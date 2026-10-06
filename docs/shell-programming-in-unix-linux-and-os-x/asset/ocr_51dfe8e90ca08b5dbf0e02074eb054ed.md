```
$ cut -d: -f1,6 /etc/passwd | tr : ' '
root /
cron /
bin /
uuucp /usr/spool/uucp
asg /
steve /users/steve
other /
$
```

Enclosed between the single quotes is a tab character (even though you can't see it—just take our word for it). It must be enclosed in quotes to keep it from being parsed and discarded by the shell as extraneous whitespace.

Working with characters that aren't printable? The octal representation of a character can be given to tr in the format \
nn

where `nnn` is the octal value of the character. This isn't used too often, but can be handy to remember.

For example, the octal value of the character is 11, so another way to accomplish the colon-to-tab transformation is to use the `tr` command

```
tr : '\11'
```

Table 3.3 lists characters that you'll often want to specify in octal format.

# Table 3.3 Octal Values of Some ASCII Characters

| Character | Octal value |
|---|---|n| Bell | 7 |
| Backspace | 10 |
| Tab | 11 |
| Newline | 12 |
| Linefeed | 12 |
| Formfeed | 14 |
| Carriage Return | 15 |
| Escape | 33 |

In the following example, `tr` takes the output from `date` and translates all spaces into newline characters. The result is that each field of output appears on a different line:

```
$ date | tr ' '\12' Translate spaces to newlines
Sun
```