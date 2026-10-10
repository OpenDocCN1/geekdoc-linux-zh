![](bbox=[0.05, 0.04, 0.86, 0.41])

Figure 11.1   The auto-mode-alist Help Window

Another associated list matches scripting-language files to major modes. Instead of using the file-name suffix, the interpreter-mode-alist matches strings found in the first line of such files. Here is a cons cell from that a-list:

```
```emacs-lisp
('"python" . Python-mode)
```

```

Python files often begin with a line such as this:

```
```python
#!/bin/env python
```

```

When such a file is loaded into an Emacs session the interpreter-mode-alist will find a match in that first line and the file will be opened in Python mode. The reasoning behind this a-list is that scripting-language files might not have a suffix which would allow auto-mode-alist to associate the file with a major mode.

# What a Mode Does for You

A mode specialized for editing certain types of files transforms Emacs into an editor optimized for that particular type of file. This is all effortless and transparent to the user. You open an HTML file, and an HTML mode comes into play, a LaTeX file is opened, and AucTeX takes over. This happens only if the file’s suffix is included in the auto-mode-alist variable. Many varieties of files are included in