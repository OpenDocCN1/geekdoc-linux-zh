# Shell Pattern-Matching Support

The shell command line allows you to use strings of specially constructed character patterns for wildcard matches. This is a different simpler capability than that supported by GNU utilities such as grep, which can use more complex patterns, known as expressions, to search through files or directories or to filter data input to or out of commands.

The shell’s pattern strings can be simple or complex, but even using a small subset of the available characters in simple wildcards can yield constructive results at the command line. Some common characters used for shell pattern matching are

+   - `*`—Matches any character. For example, to find all files in the current directory ending in `.txt`, you could use:
+   
+     ```shell
+     $ ls *.txt
+     ```
+   
+   - `?`—Matches a single character. For example, to find all files in the current directory ending in the extension `.d?c` (where ? could be 0–9, a–z, or A–Z):
+   
+     ```shell
+     $ ls *.d?c
+     ```
+   
+   - `[xxx]` or `[x-x]`—Matches a range of characters. For example, to list all files in a directory with names containing numbers,
+   
+     ```shell
+     $ ls *[0-9]*
+     ```
+   
+   - `\x`—Matches or escapes a character such as `?` or a tab character. For example, to create a file with a name containing question mark,
+   
+     ```shell
+     $ touch foo\?
+     ```

Note that the shell might not interpret some characters or regular expressions in the same manner as a Linux command, and mixing wildcards and regular expressions in shell scripts can lead to problems unless you’re careful. For example, finding patterns in text is best left to regular expressions used with commands such as grep; simple wildcards should be used for filtering or matching filenames on the command line. And although both Linux command expressions and shell scripts can recognize the backslash as an escape character in patterns, the dollar sign ($) will have two wildly different meanings (single-character pattern matching in expressions and variable assignment in scripts).

> **CAUTION**
> 
> Make sure you read your command carefully when using wildcards; an all-too-common error is to type something like `rm -rf * .txt` with a space between the `*` and the `.txt`. By the time you wonder why the command is taking so long, Bash will already have deleted most of your files. The problem is that it will treat the `*` and the `.txt` separately. `*` will match everything, so Bash will delete all your files.