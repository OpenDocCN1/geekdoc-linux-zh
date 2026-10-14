```
[me@linuxbox ~]$ vim ~/bin/sys_info_page
```

and enter the following program:

```
#!/bin/bash

# Program to output a system information page
echo "<HTML>"
echo "    <HEAD>"
echo "        <TITLE>Page Title</TITLE>"
echo "    </HEAD>"
echo "    <BODY>"
echo "        Page body."
echo "    </BODY>"
echo "</HTML>"
```

Our first attempt at this problem contains a shebang, a comment (always a good idea) and a sequence of echo commands, one for each line of output. After saving the file, we’ll make it executable and attempt to run it:

```
[me@linuxbox ~]$ chmod 755 ~/bin/sys_info_page
[me@linuxbox ~]$ sys_info_page
```

When the program runs, we should see the text of the HTML document displayed on the screen, since the echo commands in the script send their output to standard output. We’ll run the program again and redirect the output of the program to the file sys_info_page.html, so that we can view the result with a web browser:

```
[me@linuxbox ~]$ sys_info_page > sys_info_page.html
[me@linuxbox ~]$ firefox sys_info_page.html
```

So far, so good.

When writing programs, it’s always a good idea to strive for simplicity and clarity. Maintenance is easier when a program is easy to read and understand, not to mention that it can make the program easier to write by reducing the amount of typing. Our current version of the program works fine, but it could be simpler. We could actually combine all the echo commands into one, which will certainly make it easier to add more lines to the program’s output. So, let’s change our program to this: