# AccessFileName

The `AccessFileName` directive defines the name of the per-directory access control configuration file. The default name `.htaccess` has a leading period to hide the file from normal directory listing under Unix systems. The only reason to change the name to something else is to increase security by obscurity, which is not much of a reason. However, if you do change the file name to something else, make sure that you change the regular expression `"^\\.ht"` to `"^\\.whatever"` where `.whatever` is the first view character of what you set `AccessFileName` to.

# Files container

The following `<Files . . . >` container tells Apache to disallow access to any file that starts with a `.ht` (that is, the `.htaccess` or `.htpasswd`). This corresponds to the default `#AccessFileName`.

```
<Files ~ "^\\.ht"> 
    Order allow,deny
    Deny from all
</Files>
```

# UseCanonicalName

Next directive is `UseCanonicalName`, which is set to `On`. It tells Apache to create all self-referencing URLs using `$ServerName:$Port%` format. Leaving it on is a good idea.

# TypesConfig

The `TypesConfig` directive points to the mime configuration file `mime.types` that resides in the default `conf` directory. You do not need to change it unless you have relocated this file.

# DefaultType

The `DefaultType` directive sets the `Content-Type` header for any file whose MIME type cannot be determined from the file extension. For example if you have a file `%DocumentRoot%/myfile`, then Apache uses the `%DefaultType%`, which is set to `text/plain`, as the content type for the file. This means that when the Web browser requests and receives such a file in response, it will display the contents in the same way it will display a plain-text file. Now, if you think most of your unknown file contents should be treated as HTML, then use `text/html` in place of `text/plain`.

# IfModule container

The next `<IfModule . . . >` container tells Apache to enable the MIME magic module (mod_mime_magic) if it exists, and to use the `%MIMEMagicFile%` as the magic information (byte patterns) needed to identify MIME-type files. The default should be left alone unless you want to change the path of the magic file.