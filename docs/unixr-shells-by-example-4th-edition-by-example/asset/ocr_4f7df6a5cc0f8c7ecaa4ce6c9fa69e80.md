# EXAMPLE 11.19

```
1  $ FCEDIT=/usr/bin/vi
2  $ pwd
3  $ fc
<Starts up the full-screen vi editor with the pwd command on line 1>
```

![](bbox=[0.3, 0.3, 0.75, 0.55])

```
4  $ history
1 date
2 ls -l
3 echo "hello"
4 pwd
```

```
5  $ fc -3 -l    # Start vi, edit, write/quit, and execute last 3 commands.
```

# EXPLANATION

+   1 The FCEDIT variable can be assigned the pathname for any of the UNIX text editors you have on your system, such as vi, emacs, textedit, and so on. If not set, the ed editor is the default.
+   2 The pwd command is typed at the command line. It will be placed in the history file.
+   3 The fc command caused the editor (set in FCEDIT) to be invoked with the last command typed in the editor window. If the user writes and quits the editor, any commands typed there will be executed.
+   4 The history command lists recently typed commands.
+   5 The fc command is used to start up the editor with the last three commands from the history file in the editor's buffer.

# 11.4 Commenting and Filename Expansion

Filename expansion is a mechanism that allows the user to type part of a filename and press the Esc key to see the rest of the filename(s). In the following examples, [Esc] represents the Esc key.