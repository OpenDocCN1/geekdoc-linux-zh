colon (:), the shell expands the variable **a** into four words, each of which is an argu-  ment to **cat**. Now **cat** reports errors for four files: **w, x, y,** and **z**. Word splitting based  on the colon (:) takes place only *after* the variable **a** is expanded.

The shell splits all *expanded* words on a command line according to the separating  characters found in **IFS**. When there is no expansion, there is no splitting. Consider  the following commands:

```
```
$ IFS="p"
$ export VAR
```
```

Although **IFS** is set to **p**, the **p** on the **export** command line is not expanded, so the  word **export** is not split.

The following example uses variable expansion in an attempt to produce an **export**  command:

```
```
$ IFS="p"
$ aa=export
$ echo $aa
ex ort
```
```

This time expansion occurs, so the **p** in the token **export** is interpreted as a separator  (as the **echo** command shows). Next, when you try to use the value of the **aa** variable  to export the **VAR** variable, the shell parses the **$aa VAR** command line as **ex ort**  **VAR**. The effect is that the command line starts the **ex** editor with two filenames: **ort**  and **VAR**.

```
```
$ aa VAR
2 files to edit
"ort" [New File]
Entering Ex mode. Type "visual" to go to Normal mode.
E173: 1 more file to edit
:q
$
```
```

If **IFS** is unset, **bash** uses its default value (SPACE-TAB-NEWLINE). If **IFS** is null, **bash** does not  split words.

# Multiple separator characters

> **tip**  Although the shell treats sequences of multiple SPACE or TAB characters as a single separator, it  treats *each occurrence* of another field-separator character as a separator.

# CDPATH: BROADENS THE SCOPE OF cd

The **CDPATH** variable allows you to use a simple filename as an argument to the  **cd** builtin to change the working directory to a directory other than a child of the  working directory. If you typically work in several directories, this variable can  speed things up and save you the tedium of using **cd** with longer pathnames to  switch among them.