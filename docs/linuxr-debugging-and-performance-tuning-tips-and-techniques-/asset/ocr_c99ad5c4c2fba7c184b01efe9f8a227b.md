**TABLE 12.6**

wordexp() error return values

| Constant | Meaning |
| :--- | :--- |
| WRDE_BADCHAR | A metacharacter (one of newline, `' '`, `&`, `;`, `<`, `>`, `(`, `)`, `{`, `}`, or `)`) appeared in an invalid location. |
| WRDE_BADVAL | A variable was undefined and `WRDE_UNDEF` is set. |
| WRDE_CMDSUB | Command substitution was attempted and `WRDE_NOCMD` was set. |
| WRDE_NOSPACE | There was a problem allocating dynamic memory. |
| WRDE_SYNTAX | There was a shell syntax error. |

We leave it to you as an exercise (see later) to modify ch12-glob.c to use wordexp() and wordfree(). Here’s our version in action:

```
```text
$ ch12-wordexp 'echo $HOME'                Shell variable expansion
echo
/home/arnold
$ ch12-wordexp 'echo $HOME/*.gz'          Variables and wildcards
echo
/home/arnold/48000.wav.gz
/home/arnold/ipmapq-HOWTO.tar.gz
/home/arnold/rc.firewall-examples.tar.gz
$ ch12-wordexp 'echo ~arnold'             Tilde expansion
echo
/home/arnold
$ ch12-wordexp 'echo ./arnold/.p*'        Tilde and wildcards
echo
/home/arnold/.posinitnotes
/home/arnold/.procmailrc
/home/arnold/.profile
$ ch12-wordexp 'echo `~arnold/.p*``'      Quoting works
echo
~arnold/.p*
```
```

# ### 12.8 Regular Expressions

A *regular expression* is a way to describe patterns of text to be matched. If you’ve used GNU/Linux or Unix for any time at all, you’re undoubtedly familiar with regular expressions: They are a fundamental part of the Unix programmer’s toolbox. They are integral to such everyday programs as `grep`, `egrep`, `sed`, `awk`, Perl, and the `ex`, `vi`, `vim`, and Emacs editors. If you’re not at all familiar with regular expressions, we suggest