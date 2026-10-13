+   - Keys are sometimes pressed in combination; when this is the case, the keys are presented like this:
+   
+     Ctrl+h
+   
+     This example implies that you must press and hold the Ctrl key, press the *h* key, and then release both keys.

> **Note**
> 
> This book uses a convention for key names that might vary from what you are accustomed to. To avoid confusion in the case-sensitive UNIX environment, this book uses lowercase letters to refer to keys when uppercase letters might be the norm. For example, this book uses the form Ctrl+c instead of the form Ctrl+C (the latter form might make some readers wonder whether they should press Ctrl and Shift and c).

+   - Some sample listings show a portion of the screen after you type a specific command. These listings show the command prompt or shell prompt—usually a dollar sign ($)—followed by what you type in **bold monospace**. Don’t type the dollar sign when you follow the example on your own system. Consider this example:
+   
+     You should type only what appears in **bold** on the first line (that is, type `lp report.txt &` and then press Enter). The rest of the listing shows Linux’s response to the command.

```
$ lp report.txt &
3146
$
```

+   - When discussing the syntax of a Linux command, this book uses some special formatting to distinguish between the required portions and the variable portions. Consider the following example:
+   
+     In this syntax, the *filename* portion of the command is a variable; that is, it changes depending on what file you actually want the `lp` command to work with. The `lp` is required because it’s the actual command name. Variable information is presented in *italic monospace*; information that must be typed exactly is not in italic.

```
lp filename
```

+   - In some cases, command information is optional; that is, it’s not required for the command to work. Square brackets (`[ ]`) enclose optional parts of the command syntax. Consider the following example:
+   
+     Here, `lp` is the command name and is neither optional nor variable. The *device1* parameter is both variable and optional (it is in italic and enclosed in square brackets); this means that you can type any device name in place of *device1* (without the brackets), or you can type nothing at all for that parameter. The `abc` parameter is optional (you don’t have to use it if you don’t want to), but it’s not variable; if you use it, you must type it exactly as it appears in the book—again, without the brackets.

```
lp filename [device1] [abc]
```

+   - Tips, Notes, and Cautions appear throughout the book in special formats to make the information they contain easy to locate. Longer discussions not integral to the flow of the chapter are set aside as sidebars with their own headings.