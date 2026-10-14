would certainly make it easier to add more lines to the program's output. So, let's change our program to this:

```
#!/bin/bash

# Program to output a system information page
echo "<HTML>
<HEAD>
<TITLE>Page Title</TITLE>
</HEAD>
<BODY>
Page body.
</BODY>
</HTML>"
```

A quoted string may include newlines and, therefore, contain multiple lines of text. The shell will keep reading the text until it encounters the closing quotation mark. It works this way on the command line, too:

```
[me@linuxbox ~]$ echo "<HTML>
<HEAD>
> <TITLE>Page Title</TITLE>
> </HEAD>
> <BODY>
> Page body.
> </BODY>
> </HTML>"
```

The leading > character is the shell prompt contained in the PS2 shell variable. It appears whenever we type a multiline statement into the shell. This feature is a little obscure right now, but later, when we cover multiline programming statements, it will turn out to be quite handy.

# Second Stage: Adding a Little Data

Now that our program can generate a minimal document, let's put some data in the report. To do this, we will make the following changes:

```
#!/bin/bash

# Program to output a system information page
echo "<HTML>
<HEAD>
<TITLE>System Information Report</TITLE>
</HEAD>
<BODY>
<H1>System Information Report</H1>
</BODY>
</HTML>"
```

We added a page title and a heading to the body of the report.