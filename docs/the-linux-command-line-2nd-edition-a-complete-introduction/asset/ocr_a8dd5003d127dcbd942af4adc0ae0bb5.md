> conversion. They are often named using the convention of format2format. Try using the command ls /usr/bin/*[[ :alpha:]]2[[ :alpha:]]* to identify them. Also try searching for programs named formattoformat.

For our last exercise with groff, we will revisit our old friend distros.txt once more. This time, we will use the tbl program which is used to format tables to typeset our list of Linux distributions. To do this, we are going to use our earlier sed script to add markup to a text stream that we will feed to groff.

First, we need to modify our sed script to add the necessary requests that tbl requires. Using a text editor, we will change distros.sed to the following:

```
# sed script to produce Linux distributions report
1 i\
.TS\
center box;\
cb s s\
cb cb cb\
1 n c.\
Linux Distributions Report\
=\
Name Version    Released\
\
s/\([0-9]\{2\}\)\/\([0-9]\{2\}\)\/\([0-9]\{4\}\)$/\3-\1-\2/
$ a\
.TE
```

Note that for the script to work properly, care must been taken to see that the words “Name Version Released” are separated by tabs, not spaces. We’ll save the resulting file as distros-tbl.sed. tbl uses the .TS and .TE requests to start and end the table. The rows following the .TS request define global properties of the table which, for our example, are centered horizontally on the page and surrounded by a box. The remaining lines of the definition describe the layout of each table row. Now, if we run our report-generating pipeline again with the new sed script, we’ll get the following :

```
[me@linuxbox ~]$ sort -k 1,1 -k 2n distros.txt | sed -f distros-tbl.sed | groff -t -T ascii 2>/dev/null
+---------------------------------+
| Linux Distributions Report      |
+---------------------------------+
| Name    Version    Released     |
```