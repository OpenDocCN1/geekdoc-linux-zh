# UseCanonicalName

UseCanonicalName, which is typically set to On, tells Apache to create all self-referencing URLs using ServerName:Port format. Leaving it on is a good idea.

# TypesConfig

The TypesConfig directive points to the MIME configuration file mime.types that resides in the default conf directory. You do not need to change this directive unless you have relocated this file somewhere else.

# DefaultType

The DefaultType directive sets the Content-Type header for any file whose MIME type cannot be determined from the file extension. For example if you have a file DocumentRoot/myfile, Apache uses the DefaultType setting, which is text/plain, as the content type for the file. This means that when the Web browser requests and receives such a file in response, it displays the contents in the same way that it displays a plain-text file. But, for example, if you think that most of your unknown file contents should be treated as HTML you can use text/html in place of text/plain.

The next <IfModule ...> container tells Apache to enable the MIME magic module (mod_mime_magic) if it exists and to use the MIMEMagicFile as the magic information (bytes patterns) needed to identify MIME type of files. The default should be left alone unless you want to change the path of the magic file.

```
<IfModule mod_mime_magic.c>
    MIMEMagicFile conf/magic
</IfModule>
@Heading 3:HostnameLookups
```

The HostnameLookups directive tells Apache to enable DNS lookup per request if this directive is set to On. However, the default setting is Off and therefore no DNS lookup is performed to process a request, which speeds up response time. Performing a DNS lookup to resolve IP address to hostname is a time-consuming step for a busy server and should only be done using the logresolve utility. Leave the default as is.