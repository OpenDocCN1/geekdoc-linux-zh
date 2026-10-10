mally called “jython”, but if yours isn’t, or if you call it using an alias, you can set the variable py-default-interpreter to the name of your executable. You could do this with a setq statement like many of the other variable-setting statements earlier in this book, but this might be a good time to investigate the Customize buffer for Python. Press M-x and type

```
```
customize-group
```
```

Respond to the prompt with

```
```
python
```
```

Figure 16.13 shows the initial Python Customize buffer.

The first items are the names of the default Python-mode executables, both Java and C, and the one that should be set as default. Among the other settings you might take a look at are the default indentation width, whether to use various “electric” features, and whether to beep a warning when the mode has changed the tabwidth (when a Python file with a different indentation setting has been loaded).

Python-mode uses the standard font-lock faces such as function-name-face and string-face. If you have already set the font-lock faces to your liking, you shouldn’t have to do anything special for this mode.

![](bbox=[0.18, 0.61, 0.82, 0.91])

Figure 16.13  Customizing Python-mode