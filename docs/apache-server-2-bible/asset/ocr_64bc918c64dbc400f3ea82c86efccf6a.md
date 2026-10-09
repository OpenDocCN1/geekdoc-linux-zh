# **SSI Example #2**

Example of the SSI exec cgi command:

Embedded commands:

```
<!--#exec cgi="/cgi-bin/colors.pl" -->
```

Result:

| color  | swatch |
|--------|--------|
| black  |        |
| blue   |        |
| brown  |        |
| gray   |        |
| green  |        |
| red    |        |
| white  |        |
| yellow |        |

**Figure 13-3: Output of the exec_cg1.shtml file**

Note that if a CGI script returns a `Location` header instead of output, the header is translated into an HTML anchor. For example, the Listing 13-4 shows a simple Perl CGI script called `relocate.pl` that prints out a `Location:` header as the output.

# **Listing 13-4: relocate.pl**

```
#!/usr/bin/perl -w

    print 'Location: http://apache.nitetc.com' . "\n\n";

    exit 0;
```

When a Web browser requests the `exec_cg2.shtml` file, shown in Listing 13-5, the server turns the `Location:` header into an HTML anchor instead of redirecting the browser to the `http://apache.nitetc.com` site.

# **Listing 13-5: exec_cg2.shtml**

```
<HTML>
  <HEAD> <TITLE> Apache Server 2 - Chapter 13 </TITLE></HEAD>
  <BODY BGCOLOR="white">
  <FONT SIZE=+1 FACE="Arial">SSI Example #3</FONT>
```