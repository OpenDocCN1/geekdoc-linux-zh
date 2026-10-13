If you want to see debugging output for your CGI, specify cgiwrapd instead of CGIWrap, as in the following URL:

http://www.yourdomain.com/cgi-bin/cgiwrapd/username/scriptname

If the script is an nph-style script, you must run it using the following URL:

http://www.yourdomain.com/cgi-bin/nph-cgiwrapd/username/scriptname

# Reducing server-side include risks

If you run external applications using SSI commands such as exec, the security risk is virtually the same as with the CGI applications. However, you can disable this command very easily under Apache, using the Options directive as follows:

```
<Directory />
    Options IncludesNOEXEC
</Directory>
```

This disables exec and includes SSI commands everywhere on your Web space; however, you can enable these commands whenever necessary by defining a directory container with narrower scope. The following is an example:

```
<Directory />
    Options IncludesNOEXEC
</Directory>

<Directory "/ssi">
    Options +Include
</Directory>
```

This configuration segment disables the exec command everywhere but the /ssi directory.