# Configuring the Apache Server

+   AddDescription "file description" filename: Specifies that the file description string display next to the specified filename in the directory listing. You can use a wildcard, as *.html, as the filename. For example, the following directive describes files ending with .tgz GZIP compressed tar archives:

```
AddDescription "GZIP compressed tar archive" .tgz
```

+   AddIcon iconfile extension1 extension2 ... : Associates an icon with one or more file extensions. The following directive associate the icon /icons/text.gif with the file extension .txt:

```
AddIcon /icons/text.gif .txt
```

+   AddByType MIME types: Associates an icon with a group of file types as a wildcard form of MIME types (such as /* or *). To associate an icon file of /icons/text.gif with all text types, specify the following:

```
AddByType (TXT, /icons/text.gif) */*
```

This directive tells the server to use TXT in place of the icon for clients that cannot accept images. (Browsers tell the server what types of data they can accept.)

+   AddByEncoding encoding1 encoding2 ... : Specifies an icon for one or more encoding types (such as x-compress or x-zip).

+   IndexIgnore filename1 filename2 ... : Instructs the server to ignore the specified filenames (typically contain wildcards) when preparing a directory listing. To leave out README, HEADER, and all files with names with a period (.), a trailing tie (-), or a hash mark (#), specify the following:

```
IndexIgnore ??* ~ # HEADER* RCS CVS *v *t
```

+   IndexOptions option1 option2 ... : Indicates the options you want in the directory listing prepared by the server. Options can include one or more of the following:

+   * FancyIcon turns on the fancy directory listing that includes filenames and icons representing the files' sizes, types, and last-modified dates.

+   * IconHeight=N specifies that icons are N pixels tall.

+   * IconWidth=N specifies that icons are N pixels wide.

+   * NameWidth=N makes the filename column N characters wide.

+   * IconsAreLinks makes the icons act like links.

+   * ScanHTMLTitles shows a description of HTML files.

| Book VIII
Chapter 2
Running the Apache Web Server |