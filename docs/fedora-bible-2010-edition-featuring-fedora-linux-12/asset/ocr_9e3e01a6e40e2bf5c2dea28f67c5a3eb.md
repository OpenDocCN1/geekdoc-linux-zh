The `AddLanguage` directive performs similar mappings, associating a MIME language definition with a filename extension. The `LanguagePriority` directive determines the precedence if a particular file exists in several languages (and if the client does not specify a preference). Using the preceding definition, if the file `index.html` were requested from a directory that contained the files `index.html.en`, `index.html.en`, `index.html.fr`, and `index.html.it`, the `index.html.en` file would be sent to the client.

Using `LanguagePriority`, you can set which language is used in case a decision on what language to use can’t be made during content negotiation. If you are expecting multi-language use of your Web content, you should check (and probably change) the priority here.

# ### Choosing character sets

The default character set to use and character sets to use for files with particular file extensions are set using the `AddDefaultCharset` and `AddCharset` directives, respectively. The default character set of UTF-8 (as shown in the following code example) is a good choice. Other standard ISO fonts, as well as some nonstandard fonts, can be set using `AddCharset` directives.

```
AddDefaultCharset UTF-8
```

You can retrieve an official list of character sets and the file extensions that are assigned to them at `http://www.iana.org/assignments/character-sets`.

# ### Adding MIME types and handlers

With the `AddType` directive, you can enhance the MIME types assigned for your Apache Web server without editing the `/etc/mime.types` file. With the `AddHandler` directive, you can map selected file extensions to handlers (that result in certain actions¹ being taken):

```
AddType application/x-gzip .gz .tgz

AddHandler type-map var
```

# ### Defining actions and headers

Some types of media can be set to execute a script when they are opened. Likewise, certain handler names, when opened, can be set to perform specified scripts. The `Action` directive can be used to configure these scripts:

```
# Action lets you define media types that execute a script whenever
# a matching file is called. This eliminates the need for repeated URL
# pathnames for oft-used CGI file processors.
# Format: Action media/type /cgi-script/location
# Format: Action handler-name /cgi-script/location
```

The `Action` directive maps a CGI script to a handler or a MIME type, whereas the `Script` directive maps a CGI script to a particular HTTP request method (`GET`, `POST`, `PUT`, or `DELETE`). These options allow scripts to be executed whenever a file of the appropriate MIME type is requested, a handler is called, or a request method is invoked.