Notice that the `ls` output is nicely formatted using the `<PRE>` and `</PRE>` pair. If you want to output something that uses new lines, you may have to use `<PRE>` tags to keep the output readable, as shown in Figure 13-5.

# ### fsize

This command prints the size of the specified file. The syntax you use for this command depends on whether the path to the directory is relative or virtual:

```
```
 fsize file="path"
 fsize virtual="URL"
```
```

When the first syntax is used, the path is assumed to be relative to the directory containing the current SSI document being parsed. You cannot use `../` in the path, nor can absolute paths be used. You cannot access a CGI script in this fashion. You can, however, access another parsed document. For example:

```
`< ! --#fsize file="download.zip" -- >`
```

If the second syntax is used, the *virtual* path is assumed to be a (%-encoded) URL path. If the path does not begin with a slash (\/,) then it is taken to be relative to the current document. You must access a normal file this way, but you cannot access a CGI script in this fashion. Again, however, you can access another parsed document. For example:

```
`< ! --#fsize virtual="/download/free_software.zip" -- >`
```

The output format is subject to the *sizemft* format specification. See the *config* command for details.

# ### lastmod

The `lastmod` command prints the last modification date of the specified file. Again, there are two syntax options, depending on the path to the directory:

```
```
 lastmod file="path"
 lastmod virtual="URL"
```
```

The output is subject to the *timemft* format specification. For example:

```
```
< ! --#lastmod file="free_software.zip" -- >
< ! --#lastmod virtual="/download/free_software.zip" -- >
```
```

If you are unclear about the syntax difference, see the *fsize* command as an example. To control how the modification date is printed, see the *config* command.