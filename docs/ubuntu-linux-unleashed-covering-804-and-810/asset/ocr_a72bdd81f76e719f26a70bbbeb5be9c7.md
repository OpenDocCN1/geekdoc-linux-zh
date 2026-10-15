and can be read using Adobe's Acrobat Reader for Linux or the evince client. Guides are also available as bundled HTML files for reading with a web browser such as links, KDE's Konqueror, GNOME's Epiphany, or Firefox. Along with these guides, Ubuntu provides various tips, frequently asked questions (FAQs), and HOWTO documents.

You will find traditional Linux software package documentation, such as manual pages, under the /usr/share/man directory, with documentation for each installed software package under /usr/share/doc.

Linux manual pages are compressed text files containing succinct information about how to use a program. Each manual page generally provides a short summary of a command's use, a synopsis of command-line options, an explanation of the command's purpose, potential caveats or bugs, the name of the author, and a list of related configuration files and programs.

For example, you can learn how to read manual pages by using the man command to display its own manual page, as follows:

```
$ man man
```

After you press Enter, a page of text appears on the screen or in your window on the desktop. You can then scroll through the information using your keyboard's cursor keys, read, and then press the Q key to quit reading.

Many of the software packages also include separate documents known as HOWTOs that contain information regarding specific subjects or software.

If the HOWTO documents are simple text files in compressed form (with filenames ending in .gz), you can easily read the document by using the zless command, which is a text pager that enables you to scroll back and forth through documents. (Use the less command to read plain-text files.) You can start the command by using less, followed by the complete directory specification and name of the file, or pathname, like this:

```
$ less /usr/share/doc/httpd-2.0.50/README
```

To read a compressed version of this file, use the zless command in the same way:

```
$ zless /usr/share/doc/attr-2.4.1/CHANGES.gz
```

After you press Enter, you can scroll through the document using your cursor keys. Press the Q key to quit.

If the HOWTO document is in HTML format, you can simply read the information using a web browser, such as Firefox. Or if you are reading from a console, you can use the links or lynx text-only web browsers, like this:

```
$ links /usr/share/doc/stunnel-4.0.5/stunnel.html
```

The links browser offers drop-down menus, accessed by clicking at the top of the screen. You can also press the Q key to quit.