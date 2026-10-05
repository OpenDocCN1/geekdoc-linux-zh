# 15.3 Apache ApacheSSL/Stronghold

```
<LIMIT GET POST PUT>
require valid-user
</LIMIT>
```

Or in a <Directory> directive:

```
<Directory /home/web>
AuthType Basic
AuthUserFile /home/cary/etc/passwd
AuthGroupFile /dev/null
AuthName Realm of the Kazoos
<LIMIT GET POST PUT>
require valid-user
</LIMIT>
</Directory>
```

The <LIMIT> directive tells the server what HTTP methods require a valid user, in this case, GET, POST, and PUT (PUT is used for file uploading).

# CGI and SSI

The Common Gateway Interface (CGI) and Server Side Includes (SSI) are the two most common ways to execute external programs. CGI is designed to both receive and send information from and to the server. SSI is moreover; mainly it sends information. SSI can do more than simply call external programs. It can also include some simple system information such as the local time, or execute cgi.

Perl is the preemptive language for CGI programming. This is something of a double-edged sword. On the one hand, large collections of “canned” scripts for variety common CGI tasks. It also has very powerful features for processing strings, including a large set of regular expression atoms and operators. Since CGI frequently involves large amounts of text processing, this helps to fuel Perl’s popularity. On the other hand, Perl is not the easiest to learn, nor is its syntax particularly easy to read (there are obfuscated Perl contests!).

After Perl, there are several languages which are popular for use in CGI: Python, Tcl, C, and Java. Additionally there are languages which can be embedded in HTML and parsed later by a CGI program; PHP (discussed below) falls into this category. The PHP parser can also be embedded into Apache and servers based on it.

The number of books published on CGI is rather large and most cover the topic much more thoroughly than is suitable for us here. One criticism of most of the literature available is that it tends to focus nearly entirely on