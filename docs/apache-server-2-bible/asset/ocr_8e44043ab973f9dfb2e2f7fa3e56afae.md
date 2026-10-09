# Listing 3-1 (continued)

```
Order allow,deny

    Allow from all

  </Directory>

  ScriptAlias /cgi-bin/ "/usr/local/apache/cgi-bin/"

  <Directory "/usr/local/apache/cgi-bin">

    AllowOverride None

    Options None

    Order allow,deny

    Allow from all

  </Directory>

  IndexOptions FancyIndexing VersionSort

  AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip

  AddIconByType (TXT,/icons/text.gif) text/*

  # Many more AddIconByType directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  AddIcon /icons/binary.gif .bin .exe

  # Many more AddIcon directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  DefaultIcon /icons/unknown.gif

  ReadmeName README

  IndexIgnore .??* *~ \* HEADER\* README\* RCS CVS \*,v \*,t

  AddEncoding x-compress Z

  AddEncoding x-gzip .gz .tgz

  AddLanguage da .dk

  AddLanguage nl .nl

  AddLanguage en .en

  # Many more AddLanguage directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  LanguagePriority da nl et fr de el it ja kr no pl pt pt-br lts ca es sv tw

  AddDefaultCharset ISO-8859-1

  AddCharset ISO-8859-1 .iso8859-1 .latin1

  AddCharset ISO-8859-2 .iso8859-2 .latin2 .cen

  # Many more AddCharset directives follow in the

  # default httpd.conf but removed here to keep
```