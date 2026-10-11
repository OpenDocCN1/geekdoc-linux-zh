Likewise, if you needed to find a line in your /etc/ntp.conf file that contains the directive "server", you could enter `grep server /etc/ntp.conf` at the shell prompt. This is shown in the next example:

```
```
fs2:~: $ grep server /etc/ntp.conf
# server 127.127.0.0 mode 5 prefer
server 127.127.1.0
## # ntpct addserver cyourserver
server bigben.cac.washington.edu iburst
# key (7) for accessing server variables
# controlkey 15
				# key (6) for accessing server variables
fs2:~: $
```
```

When working with grep at the command line, you can use the following options:

+   * **-i**	Ignores case when searching for the search text.
+   * **-l**	Displays only the names of the files that contain matching text. It doesn’t display the actual matching line of text.
+   * **-n**	Displays matching line numbers.
+   * **-r**	Searches recursively through subdirectories of the path specified.
+   * **-v**	Displays all lines that do not contain the search string.

The grep utility works great when you need to search for a specific text string within a file. However, there may be times when you need to search for more complex patterns. In this situation, you can use the egrep command instead.

> **NOTE** The egrep command is the same as using the grep -E command.

The key advantage of egrep is that it can search files for extended *regular expressions*. Regular expressions are strings consisting of *metacharacters* and *literals*.

> **NOTE** Literals are regular characters (A–Z, a–z) and numerals.

*Metacharacters* are characters that do not represent themselves but instead represent other characters. They can also be used to specify a character’s location within a text string. Some commonly used regular expressions are listed in Table 4-6. See the regex(7) man page for more information.

In addition to egrep, you can also use the fgrep (fixed-string grep) utility to search for content within files.

> **NOTE** Running fgrep is the same as running grep -F.