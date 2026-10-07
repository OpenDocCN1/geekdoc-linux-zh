# Chapter 10: Basic Scripting and Forms 263

![](bbox=[0.042, 0.093, 0.574, 0.29])

Figure 10-7: This simple selection list displays as a pop-up menu because the height is 1 and MULTIPLE selection is not enabled.

A couple of things to note about using selection lists: the first item is listed the first one displayed in the browser. This will be the only item seen in a list with a SIZE= 1 so you might consider using a first of something like "Click to choose a size" even though no one will select as their choice (use SELECTED a different option to define a default).

Note also that there are no <P> tags or other tags between the <OPTION> tags. Also, the label for each menu item can contain spaces and other characters, be certain that your script can handle these name-value pairs. Most other values do not have spaces. If you create a MULTIPLE selection list for the single name associated with the selection list. For example, in the following form (shown in Figure 10-8):

```
<SELECT NAME=OS_TYPE SIZE= 3 MULTIPLE>
<OPTION>Select Systems at your facility
<OPTION>Linux
<OPTION>Solaris
<OPTION>Other UNIX
<OPTION>Windows NT
<OPTION>Windows 95
<OPTION>Windows 3.1/3.11
<OPTION>Macintosh
</SELECT>
```

The name-value pair might be something like the following:

OS_TYPE= Linux, Solaris, Macintosh