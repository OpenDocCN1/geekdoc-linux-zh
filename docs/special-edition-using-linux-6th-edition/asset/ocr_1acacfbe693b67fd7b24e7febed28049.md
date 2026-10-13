The following line adds a new file type for files with the extension .mdoc:

```
AddType text/x-mdoc mdoc
```

In situations in which you cannot use file extensions to identify the files on your system, you can use content-based file typing. This system tries to identify a file’s type based on whether small strings or sequences of bytes can be found in the file at particular offsets. These matching rules are defined in a file called the magic file.

Content-based file typing is not turned on in the default Web server configuration files. Use the LoadModule directive to load the magic module:

```
LoadModule mod_mime_magic
```

To modify the magic file to support additional file types based on content, see the magic man page, which describes the syntax that is used for defining entries in this file.

# DEFINING ENCODINGS AND LANGUAGES

Some browsers are capable of more intelligent handling of a file if they know the file’s encoding. The encoding of a file is the way the file is formatted, and includes things such as whether the file is compressed and which character set is used for the file.

You can define encodings for files using the AddEncoding directive, which defines a MIME encoding based on the extension of the file. The default encodings that are specified in httpd.conf are as follows:

```
AddEncoding x-gzip gz tgz
AddEncoding x-compress Z
```

Content-based encodings can also be defined in the magic file. See the previous section for a description of this file.

Unless you have a good understanding of how encodings are interpreted by browsers, you probably need to leave these definitions alone.

The Web server can indicate the language of a file to the client, using definitions created with the AddLanguage directive. This feature can be used by add-on server modules to select the correct file to deliver to a client based on its language preference (this is called content negotiation). Use the AddLanguage directive to assign a language code to a file, based on a portion of the file’s name. For example, the following lines define the file page.en.html as an English HTML file:

```
AddFileType    text/html        html
AddLanguage    en    .en
```

# REDIRECTING CLIENTS TO MOVED FILES

The Web is a dynamic place. Web sites undergo constant revision and maintenance to keep up with new developments and needs. Because of this, it is very common for files to be moved around in the document tree (or even to other Web sites). The Web server is capable of notifying a client of a new location for a file by sending the client a redirect response.