tab width is set to whatever width was used by the file's author, ensuring that any additions you make to the file will fit in with the file's native indentation format. When you write a new Python file, the default four-space tab width is used, but this variable can be changed with Customize.

# ## Execution Commands

There are several ways to execute Python code in this mode. You can hand over the entire buffer to the interpreter by pressing Ctrl-c. A new window opens, showing you the output of the process (see Figure 16.12). A shell window running Python can be summoned, giving you an interactive Python session. The advantage of running this session in an Emacs window is that you can copy regions from another Python buffer and submit these chunks directly to the interpreter.

# ## Customization

Among the many settings you can set in the Python Group Customize buffer is the name of the python executable you are using. In most cases, this is the default, “python,” but a new version of Python written in Java has recently been gaining popularity. Python-mode makes a usually accurate guess as to which one you are using the first time you open a Python file. The Java-Python executable is nor-

![](bbox=[0.08, 0.54, 0.5, 0.95])