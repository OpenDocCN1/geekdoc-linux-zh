# AddIcon

The `AddIcon` directive enables you to assign icons to files and directory names that are displayed for ` FancyIndexing`.

+   * **Syntax:** `AddIcon icon name file [filename ...]`
+   * **Context:** Server config, virtual host, directory, per-directory access control file (`.htaccess`)
+   * **Override:** `Indexes`

For example, the following directive tells Apache to show `/icons/picture.gif` next to files that have extensions such as `.gif`, `.jpg`, and `.bmp`:

```
AddIcon /icons/picture.gif .gif .jpg .bmp
```

If you also want to provide alternative text for the file extension listed, you can use a format such as the following, where IMG is the alternative text displayed for non-graphical browsers:

```
AddIcon (IMG. /icons/picture.gif) .gif .jpg .bmp
```

If you want to display an icon for a directory, you can use the directive as follows:

```
AddIcon /path/to/your/directory/icon ^^DIRECTORY^^
```

Similarly, if you want to display an icon for each blank line displayed by the fancy indexing scheme, you can use:

```
AddIcon /path/to/your/blank/line/icon ^^BLANKICON^^
```

# AddIconByEncoding

The `AddIconByEncoding` directive lets you assign icons to `MIME-encodings`. In other words, you can assign an icon image to a `MIME type`.

+   * **Syntax:** `AddIconByEncoding icon_file MIME_encoding [MIME_encoding ...]`
+   * **Context:** Server config, virtual host, directory, per-directory access control file (`.htaccess`)
+   * **Override:** `Indexes`

For example, the following `AddIconByEncoding` directive tells Apache to display `/icons/zip.gif` icon for all files that are x-gzip (i.e. `.gz` extension) `MIME type` files.

```
AddIconByEncoding /icons/zip.gif x-gzip
```