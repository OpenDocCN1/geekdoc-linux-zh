
Line 7 defines `myname`, which points to the program’s name; this variable is for error messages from `globerr()`, defined on lines 11–15.

Lines 33–45 are the heart of the program. They loop over the patterns given on the command line, calling `glob()` on each one to append its results to the list. Most of the loop is error handling (lines 36–44). Lines 47–48 print the resulting list, and lines 50–51 clean up and return.

Lines 39–41 aren’t pretty; a separate function that converts the integer constant to a string should be used; we’ve done it this way primarily to save space. Code like this is tolerable in a small program, but a larger program should use a function.

If you think about all the work going on under the hood (opening and reading directories, matching patterns, dynamic allocation to grow the list, sorting the list), you can start to appreciate how much `glob()` does for you! Here are some results:

```
$ ch12-glob '/usr/lib/*\.so' .../*\.texi'
/usr/lib/xchat-autoS.so
/usr/lib/xchat-autoGS.so
.../00-prefix.texi
.../01-intro.texi
.../02-cmdline.texi
.../03-memory.texi
...
```

Note that we have to quote the arguments to keep the shell from doing the expansion!

> **Globbing? What’s That?**
>
> In days of yore, circa V6 Unix, the shell used a separate program to perform wildcard expansion behind the scenes. This program was named /etc/glob, and according to the V6 source code,¹ the name “glob” is short for “global.”
>
> The verb “to glob” thus passed into the Unix lexicon, with the meaning “to perform wildcard expansion.” This in turn gives us the function names `glob()` and `globfree()`. The usually understated sense of humor that occasionally peeked through from the Unix manual therefore lives on, formally enshrined in the POSIX standard. (Can you imagine anyone at IBM, in the 1970s or 1980s, naming a system routine `glob()`?)

### 12.7.3 Shell Word Expansion: wordexp() and wordfree()

Many members of the POSIX committee felt that glob() didn’t do enough: They wanted a library routine capable of doing everything the shell can do: tilde expansion (`echo $~arndld`), shell variable expansion (`echo $HOME`), and command substitution (`echo $(cd ; pwd)`). Many others felt that glob() wasn’t the right function for this purpose. To “satisfy” everyone, POSIX supplies an additional two functions that do everything:

```
#include <wordexp.h>   POSIX
int wordexp(const char *words, wordexp_t *pwordexp, int flags);
void wordfree(wordexp_t *pwordexp);
```

These functions work similarly to glob() and globfree(), but on a wordexp_t structure:

```
typedef struct {
    size_t we_wordc;      /* Count of words matched */
    char **we_wordv;      /* List of expanded words */
    size_t we_offs;       /* Slots to reserve in we_wordv */
} wordexp_t;
```

The members are completely analogous to those of the glob_t described earlier; we won’t repeat the whole description here.

As with glob(), several flags control wordexp()’s behavior. The flags are listed in Table 12.5.

**Table 12.5**
Flags for wordexp()

| Constant | Meaning |
| :--- | :--- |
| WRDE_APPEND | Append current call’s results to those of a previous call. |
| WRDE_DOFFS | Reserve we_offs spots at the front of we_wordv. |
| WRDE_NOCMD | Don’t allow command substitution. |
| WRDE_REUSE | Reuse the storage already pointed to by we_wordv. |
| WRDE_SHOWERR | Don’t be silent about errors during expansion. |
| WRDE_UNDEF | Cause undefined shell variables to produce an error. |

The return value is 0 if everything went well or one of the values in Table 12.6 if not.

**Table 12.6**
wordexp() error return values

| Constant | Meaning |
| :--- | :--- |
| WRDE_BADCHAR | A metacharacter (one of newline, `' '`, `&`, `;`, `<`, `>`, `(`, `)`, `{`, `}`, or `)`) appeared in an invalid location. |
| WRDE_BADVAL | A variable was undefined and `WRDE_UNDEF` is set. |
| WRDE_CMDSUB | Command substitution was attempted and `WRDE_NOCMD` was set. |
| WRDE_NOSPACE | There was a problem allocating dynamic memory. |
| WRDE_SYNTAX | There was a shell syntax error. |

We leave it to you as an exercise (see later) to modify ch12-glob.c to use wordexp() and wordfree(). Here’s our version in action:

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

## 12.8 Regular Expressions

A *regular expression* is a way to describe patterns of text to be matched. If you’ve used GNU/Linux or Unix for any time at all, you’re undoubtedly familiar with regular expressions: They are a fundamental part of the Unix programmer’s toolbox. They are integral to such everyday programs as `grep`, `egrep`, `sed`, `awk`, Perl, and the `ex`, `vi`, `vim`, and Emacs editors. If you’re not at all familiar with regular expressions, we suggest you take a detour to some of the books or URLs named in Section 12.9, “Suggested Reading,” page 480.

POSIX defines two flavors of regular expressions: *basic* and *extended*. Programs such as `grep`, `sed`, and the `ed` line editor use basic regular expressions. Programs such as `egrep` and `awk` use extended regular expressions. The following functions give you the ability to use either flavor in your programs:

```
#include <sys/types.h> 
#include <regex.h> 
int regcomp(regex_t *preg, const char *regex, int cflags); 
int regexec(const regex_t *preg, const char *string, size_t nmatch, 
regmatch_t pmatch[], int eflags); 
size_t regerror(int errcode, const regex_t *preg, 
char *errbuf, size_t errbuf_size); 
void regfree(regex_t *preg)
```

![](img/766b5597246d532412fad21b1c59ccec_504_0.png)

To do regular expression matching, you must first *compile* a string version of the regular expression. Compilation converts the regular expression into an internal form. The compiled form is then *executed* against a string to see whether it matches the original regular expression. The functions are as follows:

```
int regcomp(regex_t *preg, const char *regex, int cflags)
```

Compiles the regular expression `regex` into the internal form, storing it in the `regex_t` structure pointed to by `*preg`. `cflags` controls how the compilation is done; its value is 0 or the bitwise OR of one or more of the flags in Table 12.7.

```
int regexec(const regex_t *preg, const char *string, size_t nmatch, 
regmatch_t pmatch[], int eflags)
```

Executes the compiled regular expression in `*preg` against the string `string`. `eflags` controls how the execution is done; its value is 0 or the bitwise OR of one or more of the flags in Table 12.8. We discuss the other arguments shortly.

```
size_t regerror(int errcode, const regex_t *preg, char *errbuf, 
size_t errbuf_size)
```

Converts an error returned by either `regcomp()` or `regexec()` into a string that can be printed for a human to read.

```
void regfree(regex_t *preg)
```

Frees dynamic memory used by the compiled regular expression in `*preg`.

The <regex.h> header file defines a number of flags. Some are for use with regcomp(); others are for use with regexec(). However, they all start with the prefix 'REG'. Table 12.7 lists the flags for regular expression compilation with regcomp().

**Table 12.7**
Flags for regcomp()

| Constant | Meaning |
| :--- | :--- |
| REG_EXTENDED | Use extended regular expressions. The default is basic regular expressions. |
| REG_ICASE | Matches with regexec() ignore case. |
| REG_NEWLINE | Operators that can match any character don't match newline. |
| REG_NOSUB | Subpattern start and end information isn't needed (see text). |

The flags for regular expression matching with regexec() are given in Table 12.8.

**Table 12.8**
Flags for regexec()

| Constant | Meaning |
| :--- | :--- |
| REG_NOTBOL | Don't allow the ^ (beginning of line) operator to match. |
| REG_NOTEOL | Don't allow the $ (end of line) operator to match. |

The REG_NEWLINE, REG_NOTBOL, and REG_NOTEOL flags interact with each other. It's a little complicated, so we take it one step at a time.

- When REG_NEWLINE is not included in cflags, the newline character acts like an ordinary character. The '.' (match any character) metacharacter can match it, as can complemented character lists ('^ . . .'). Also, $ does not match immediately before an embedded newline, and ^ does not match immediately after one.
- When REG_NOTBOL is set in eflags, the ^ operator does not match the beginning of the string. This is useful when the string parameter is the address of a character in the middle of the text being matched.
- Similarly, when REG_NOTEOL is set in eflags, the $ operator does not match the end of the string.
- When REG_NEWLINE is included in cflags, then:
