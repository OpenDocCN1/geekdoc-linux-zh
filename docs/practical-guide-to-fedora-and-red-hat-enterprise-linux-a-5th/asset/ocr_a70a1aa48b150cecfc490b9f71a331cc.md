IgnoreClient: Ignores options the client supplied in the URL.

NameWidth=n: Sets the width of the filename column to n characters. Use * in place of n to accommodate the widest filename.

ScanHTMlTitles: Extracts and displays titles from HTML documents. Use only with FancyIndexing. Not normally used because it is CPU and disk intensive.

SuppressColumnSorting: Suppresses clickable column headings that can be used for sorting columns. Use only with FancyIndexing.

SuppressDescription: Suppresses file descriptions. Use only with FancyIndexing.

SuppressHTMLPreamble: Suppresses the contents of the file specified by the HeaderName directive, even if that file exists.

SuppressIcon: Suppresses icons. Use only with FancyIndexing.

SuppressLastModified: Suppresses the modification date. Use only with FancyIndexing.

SuppressRules: Suppresses horizontal lines. Use only with FancyIndexing.

SuppressSize: Suppresses file sizes. Use only with FancyIndexing.

VersionSort: Sorts version numbers (in filenames) in a natural way; character strings, except for substrings of digits, are not affected.

As an example, suppose a client requests a URI that points to a directory (such as http://www.example.com/support/) and none of the files specified by the DirectoryIndex directive (page 853) is present in that directory. If the directory hierarchy is controlled by a .htaccess file and AllowOverride (page 869) has been set to allow indexing, then Apache displays a directory listing according to the options specified by this directive.

When this directive appears more than once within a directory, Apache merges the options from the directives. Use + and - to merge options with options from higher-level directories. (Unless you use + or - with all options, Apache discards any options set in higher-level directories.) For example, the following directives and containers set the options for /custsup/download to VersionSort; Apache discards FancyIndexing and IgnoreCase in the download directory because there is no + or - before VersionSort in the second <Directory> container:

```
<Directory /custsup>
    IndexOptions FancyIndexing
    IndexOptions IgnoreCase
</Directory>

<Directory /custsup/download>
    IndexOptions VersionSort
</Directory>
```

Because + appears before VersionSort, the next directives and containers set the options for /custsup/download to FancyIndexing, IgnoreCase, and VersionSort: