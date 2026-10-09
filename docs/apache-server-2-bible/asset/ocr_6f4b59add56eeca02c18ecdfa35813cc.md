+   Because of a mistake in the early stages of Apache development, the proxy control is still done with the `<Directory>` container, even though the `<Location>` container is more appropriate. This may be corrected in a future version. However, this really doesn't cause any harm, other than making things a bit more difficult to conceptualize.

The `<VirtualHost>` container is discussed in a separate section, later in this chapter.

![](bbox=[0.1, 0.23, 0.21, 0.31])

# <Directory>

The `<Directory>` and `</Directory>` container tags are used to enclose a group of directives that apply only to the named directory and its subdirectories. Any directive that is allowed in a directory context may be used. The argument can be a fully qualified pathname.

**Syntax:** `<Directory directory>` ... `</Directory>`

**Default setting:** None

**Context:** Server config, virtual host

In the following example the directory `/www/mycompany/public/htdocs/download` is used as a fully qualified pathname. This example enables directory indexing in this directory.

```
`<Directory /www/mycompany/public/htdocs/download>`
`Options +Indexes`
`</Directory>`
```

You can also use wildcard characters in specifying the path. In the following example, the `?` will match any single character:

```
`<Directory /www/mycompany/public/htdocs/downloa?>`
`Options +Indexes`
`</Directory>`
```

Therefore, directories such as `/www/mycompany/public/htdocs/download` and `/www/mycompany/public/htdocs/downloa` will be matched. You can also use `*` (asterisk) to match any sequence of characters other than the `/` (slash) character. Extended regular expressions can also be used by adding the `~` (tilde) character. For example:

```
`<Directory ~ "^/www/.*/">`
```

would match any subdirectory under `/www/`. Note that regular expression-based `<Directory>` containers may not be applied until all normal (that is, without regular expression) `<Directory>` containers and `.htaccess` files have been applied.