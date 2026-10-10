
## Branches and Back References

Basic regular expressions also differ from extended regular expressions in another important aspect: an extended regular expression can be divided into branches, each one an independent regular expression. Branches are separated by | and the combined regular expression will match anything that corresponds to any of the branches. For example, `he|him` will match if either substring `he` or `him` are found in the string being examined. Basic regular expressions interpret `|` as a literal character. However, most programs supporting basic regular expressions will allow branches with `\|`.

An extended regular expression enclosed in `()` can be used in a back reference. For example, `([…]digit:]+) \1` will match any regular expression that repeats itself at least once, because the `\1` in the expression is the back reference to the piece matched by the first parenthesized subexpression. If more than one parenthesized subexpression exist in the regular expression, they can be referenced with `\2`, `\3` and so on.

For basic REs, subexpressions must be enclosed by `\( \)`, with `( )` by themselves ordinary characters. The back reference indicator is used like in extended regular expressions.

## Searching with Regular Expressions

The immediate benefit offered by regular expressions is to improve searches on filesystems and in text documents. The `-regex` option of command `find` allows to test every path in a directory hierarchy against a regular expression. For example,

```sh
$ find $HOME -regex '.* / .*' -size +100M
```

searches for files greater than 100 megabytes (100 units of 1048576 bytes), but only in paths inside the user’s home directory that do contain a match with `.* / .*`, that is, a `/` surrounded by any other number of characters. In other words, only hidden files or files inside hidden directories will be listed, regardless of the position of `/` in the corresponding path. For case insensitive regular expressions, the `-iregex` option should be used instead:

```sh
$ find /usr/share/fonts -regextype posix-extended -iregex '
.*(dejavu|liberation).*sans.*(italic|oblique).*'
/usr/share/fonts/dejavu/DejaVuSansCondensed-BoldOblique.ttf
/usr/share/fonts/dejavu/DejaVuSansCondensed-Oblique.ttf
/usr/share/fonts/dejavu/DejaVuSans-BoldOblique.ttf
/usr/share/fonts/dejavu/DejaVuSans-Oblique.ttf
/usr/share/fonts/dejavu/DejaVuSansMono-BoldOblique.ttf
/usr/share/fonts/dejavu/DejaVuSansMono-Oblique.ttf
/usr/share/fonts/liberation/LiberationSans-BoldItalic.ttf
/usr/share/fonts/liberation/LiberationSans-Italic.ttf
```

In this example, the regular expression contains branches (written in *extended* style) to list only specific font files under the `/usr/share/fonts` directory hierarchy. Extended regular expressions are not supported by default, but `find` allows for them to be enabled with `-regextype posix-extended` or `-regextype egrep`. The default RE standard for `find` is *findutils-default*, which is virtually a basic regular expression clone.

It is often necessary to pass the output of a program to command `less` when it doesn't fit on the screen. Command `less` splits its input in pages, one screenful at a time, allowing the user to easily navigate the text up and down. In addition, `less` also allows a user to perform regular expression based searches. This feature is notably important because `less` is the default paginator used for many everyday tasks, like inspecting journal entries or consulting manual pages. When reading a manual page, for instance, pressing the `/` key will open a search prompt. This is a typical scenario in which regular expressions are useful, as command options are listed just after a page margin in the general manual page layout. However, the same option might appear many times through the text, making literal searches unfeasible. Regardless of that, typing `^[[ :blank:] ]*-[o-O]` —or more simply: `^ *-[o-O]`— in the search prompt will jump immediately to option the `-o` section (if it exists) after pressing Enter, thus allowing one to consult an option description more rapidly.

## Guided Exercises

- 1. What extended regular expression would match any email address, like `info@example.org`?
- 2. What extended regular expression would only match any IPv4 address in the standard dotted-quad format, like `192.168.15.1`?
- 3. How can the `grep` command be used to list the contents of file `/etc/services`, discarding all comments (lines starting with #)?
- 4. The file `domains.txt` contains a list of domain names, one per line. How would the `egrep` command be used to list only `.org` or `.com` domains?

## Explorational Exercises

- 1. From the current directory, how would the `find` command use an extended regular expression to search for all files not containing a standard file suffix (file names not ending in `.txt` or `.c`, for example)?
- 2. Command `less` is the default paginator for displaying long text files in the shell environment. By typing `/`, a regular expression can be entered in the search prompt to jump to the first corresponding match. In order to stay in the current document position and only highlight the corresponding matches, what key combination should be entered at the search prompt?
- 3. In `less`, how would it be possible to filter the output so only lines which match a regular expression get displayed?

## Summary

This lesson covers the general Linux support for regular expressions, a widely used standard whose pattern matching capabilities are supported by most text related programs. The lesson goes through the following steps:

- What a regular expression is.
- The main components of a regular expression.
- The differences between regular and extended regular expressions.
- How to perform simple text and file searches using regular expressions.

## Answers to Guided Exercises

- 1. What extended regular expression would match any email address, like `info@example.org`?

```
egrep "\S+@\S+\.\S+"
```

- 2. What extended regular expression would only match any IPv4 address in the standard dotted-quad format, like `192.168.15.1`?

```
egrep "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}"
```

- 3. How can the `grep` command be used to list the contents of file `/etc/services`, discarding all comments (lines starting with #)?

```
grep -v ^# /etc/services
```

- 4. The file `domains.txt` contains a list of domain names, one per line. How would the `egrep` command be used to list only `.org` or `.com` domains?

```
egrep "\.org$|\.com$" domains.txt
```

## Answers to Explorational Exercises

1.  From the current directory, how would the `find` command use an extended regular expression to search for all files not containing a standard file suffix (file names not ending in `.txt` or `.c`, for example)?

```
find . -type f ! -regex '.*\.[[:alnum:]]{1,}$'
```

2.  Command `less` is the default paginator for displaying long text files in the shell environment. By typing `/`, a regular expression can be entered in the search prompt to jump to the first corresponding match. In order to stay in the current document position and only highlight the corresponding matches, what key combination should be entered at the search prompt?

Pressing Ctrl + k before entering the search expression.

3.  In `less`, how would it be possible to filter the output so only lines which match a regular expression get displayed?

By pressing `&` and entering the search expression.

![](img/824749d5fc1d265354d0e66a01af9ced_381_0.png)

## 103.7 Lesson 2

| Certificate | LPIC-1 |
| :--- | :--- |
| Version | 5.0 |
| Topic | 103 GNU and Unix Commands |
| Objective | 103.7 Search text files using regular expressions |
| Lesson | 2 of 2 |

## Introduction

Streaming data through a chain of piped commands allows for the application of compound filters based on regular expressions. Regular expressions are an important technique used not only in system administration, but also in data mining and related areas. Two commands are specially suited to manipulate files and text data using regular expressions: `grep` and `sed`. `grep` is a pattern finder and `sed` is a stream editor. They are useful by themselves, but it is when working together with other processes that they stand out.

## The Pattern Finder: grep

One of the most common uses of `grep` is to facilitate the inspection of long files, using the regular expression as a filter applied to each line. It can be used to show only the lines starting with a certain term. For example, `grep` can be used to investigate a configuration file for kernel modules, listing only option lines:

```
$ grep 'options' /etc/modprobe.d/alsa-base.conf
options snd-pcsp index=-2
options snd-usb-audio index=-2
```
