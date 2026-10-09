On my Apache server, I specified only the cgi extension as a CGI script; therefore, I renamed my CgiWrap executable to cgiwrap.cgi to get it to work. If you have similar restrictions, you might try this approach or make a link instead.

Now, execute a CGI script as follows:

```
http://www.yourdomain.com/cgi-bin/cgiwrap/username/scriptname
```

To access user kabir's CGI script test.cgi on the wormhole.nitec.com site, for example, I would use the following:

```
http://wormhole.nitec.com/cgi-bin/cgiwrap/kabir/test.cgi
```

If you want to see debugging output for your CGI, specify cgiwrapd instead of cgiwrap, as in the following URL:

```
http://www.yourdomain.com/cgi-bin/cgiwrapd/username/scriptname
```

If the script is an nph-style script, you must run it using the following URL:

```
http://www.yourdomain.com/cgi-bin/nph-cgiwrap/username/scriptname
```

# ## Hiding clues about your CGI scripts

When a vandal scans a Web site for possible holes, the vandal looks for little things that provide clues about the underlying hardware and software used for the Web site. So, the fewer clues you provide about your system, the greater the chance that your Web site will not become the vandal's next victim. There are several ways to hide some of the important details that could become clues.

# ### Use a nonstandard script alias

Use of cgi-bin alias is very popular. As soon as you see a URL with cgi-bin you know the site runs CGI scripts of some sort. This alias is set using the ScriptAlias directive in Apache's httpd.conf file. For example:

```
ScriptAlias "/cgi-bin/ " "/path/to/real/cgi/directory/"
```

But only few people realize that you can use anything to create an alias like this. For example:

```
ScriptAlias "/apps/ " "/path/to/real/cgi/directory/"
```

Now the apps in a URL serves the same purpose as cgi-bin. So, if you use something similar to:

```
ScriptAlias "/dcon/ " "/path/to/real/cgi/directory/"
```