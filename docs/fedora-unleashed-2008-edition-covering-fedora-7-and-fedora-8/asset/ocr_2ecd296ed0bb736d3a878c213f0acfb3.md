Each module adds new directives that can be used in your configuration files. As you might guess, there are far too many extra commands, switches, and options to describe them all in this chapter. The following sections briefly describe a subset of those modules available with Fedora's Apache installation.

# mod_access

mod_access controls access to areas on your web server based on IP addresses, hostnames, or environment variables. For example, you might want to allow anyone from within your own domain to access certain areas of your web. Refer to the "File System Authentication and Access Control" section earlier in this chapter for more information.

# mod_alias

mod_alias manipulates the URLs of incoming HTTP requests, such as when redirecting a client request to another URL. It also can map a part of the file system into your web hier-
archy. For example,

```
Alias /images/ /home/wsb/graphics/
```

fetches contents from the /home/wsb/graphics directory for any URL that starts with /images/. This is done without the client knowing anything about it. If you use a redirec-
tion, the client is instructed to go to another URL to find the requested content. More advanced URL manipulation can be accomplished with mod_rewrite.

# mod_asis

mod_asis is used to specify, in fine detail, all the information to be included in a response. This completely bypasses any headers Apache might have otherwise added to the response. All files with an .asis extension are sent straight to the client without any changes.

As a short example of the use of mod_asis, assume that you've moved content from one location to another on your site. Now you must inform people who try to access this resource that it has moved, as well as automatically redirect them to the new location. To provide this information and redirection, you can add the following code to a file with an .asis extension:

```
Status: 301 No more old stuff!
Location: http://gnu1ix.org/newstuff/
Content-type: text/html

<HTML>
<HEAD>
<TITLE>We've moved...</TITLE>
</HEAD>
<BODY>
<P>We've moved the old stuff and now you'll find it at:</P>
```