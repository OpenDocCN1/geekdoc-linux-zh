```
</IfModule>

# 
# AddHandler: allows you to map certain file extensions to "handlers",
# actions unrelated to filetype. These can be either built into the
# server or added with the Action command (see below)
#
# If you want to use server side includes, or CGI outside
# ScriptAliased directories, uncomment the following lines.
# To use CGI scripts:
#
#AddHandler cgi-script .cgi
#
# To use server-parsed HTML files
#
AddType text/html .shtml
AddHandler server-parsed .shtml

#
# Uncomment the following line to enable Apache's send-as-is HTTP file
# feature
#
#AddHandler send-as-is asis

#
# If you wish to use server-parsed imagemap files, use
#
AddHandler imap-file map

#
# To enable type maps, you may want to use
#
#AddHandler type-map var
```

# ## Defining actions and headers

Some types of media can be set to execute a script when they are opened. Likewise, certain handler names, when opened, can be set to perform specified scripts. The Action directive can be used to configure these scripts:

```
# Action lets you define media types that execute a script whenever
# a matching file is called. This eliminates the need for repeated URL
# pathnames for oft-used CGI file processors.
# Format: Action media/type /cgi-script/location
# Format: Action handler-name /cgi-script/location

# MetaDir: specifies the name of the directory in which Apache can find
```