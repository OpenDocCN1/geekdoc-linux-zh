The following command uses `find` to locate files with the name **README** in the directory tree with its root at the working directory. This list of files is standard out	ext{put} of `find` and becomes the list of arguments to `ls`.

```
$ ls -l $(find . -name README -print)
```

The next command line shows the older `\`command`\` syntax:

```
$ ls -1 `find . -name README -print`
```

One advantage of the newer syntax is that it avoids the rather arcane rules for token handling, quotation mark handling, and escaped back ticks within the old syntax. Another advantage of the new syntax is that it can be nested, unlike the old syntax. For example, you can produce a long listing of all **README** files whose size exceeds the size of ./README with the following command:

```
$ ls -l $(find . -name README -size +$(echo $(cat ./README) wc -c) ) -print )
```

Try giving this command after giving a set -x command (page 900) to see how bash expands it. If there is no README file, you just get the output of ls -l. For additional scripts that use command substitution, see pages 896, 915, and 945.

# $(( Versus $(

> tip The symbols $(( constitute a separate token. They introduce an arithmetic expression, not a command substitution. Thus, if you want to use a parenthesized subshell (page 293) within $( ), you must insert a SPACE between the $ ( and the next (

# **WORD SPLITTING**

The results of parameter and variable expansion, command substitution, and arithmetic expansion are candidates for word splitting. Using each character of IFS (page 309) as a possible delimiter, bash splits these candidates into words or tokens. If IFS is unset, bash uses its default value (SPACE-TAB-NEWLINE). If IFS is null, bash does not split words.

# **PATHNAME EXPANSION**

Pathname expansion (page 243), also called *filename generation* or *globbing*, is the process of interpreting ambiguous file references and substituting the appropriate list of filenames. Unless no glo (page 341) is set, the shell performs this function when it encounters an ambiguous file reference — a token containing any of the quoted characters \*?[]|. If bash cannot locate any files that match the specified pattern, the token with the ambiguous file reference is left alone. The shell does not delete the token or replace it with a null string but rather passes it to the program as is (except see no glob on page 341).

In the first echo command in the following example, the shell expands the ambiguous file reference tmp* and passes three tokens (tmp1, tmp2, and tmp3) to echo. The echo builtin displays the three filenames it was passed by the shell. After rm