```
but there will be times when proper documentation really
saves your day.</para>

<sect1 id="environment">
<title>Environment</title>
<para>There are a lot of settings concerning the environment
variables on a system, which likely will give you a headache,
to say the least.</para>
<sect2 id="env_path">
<title>The <userinput>$PATH</userinput> variable</title>
<para>If the <envar>$PATH</envar> variable looks like
this:</para>
<screen>
...

```

In Listing A.9, sed is instructed to search for lines containing <sect1>. If the string is found, then sed outputs a blank line and the line found afterwards. Because the processing is performed on the files as a stream, the size of the file is of no concern to you. If the program you use to process the XML file later should not be able to cope with the additional blank lines, then you could use the command sed '/^$/d' to erase those blank lines. You just need to be aware of the fact that this command will delete all blank lines in the stream.

# A.3.2 Removing Leading Blanks and Tabs

If you should receive a text file that contains leading blanks or Tab characters and you need to get rid of them, sed can be used to do so. Listing A.10 demonstrates how. Please note that the character string between the "[ ]" characters needs to be typed in as space, Ctrl-V, Tab.

# LISTING A.10 Removing Leading Whitespace

```
erikk@unixhost> cat leadwhite.txt
This is line 1.
    This is line 2.
        This is line 3.

This is line 4.
    This is line 5.
This is line 6.

erikk@unixhost> sed 's/[  ]*//' leadwhite.txt
This is line 1.
This is line 2.
This is line 3.
```