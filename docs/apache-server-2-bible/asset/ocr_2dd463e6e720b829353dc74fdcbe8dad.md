```
```
<HR SIZE=1>
<P> Example of the SSI <STRONG>exec cgi</STRONG> command: </P>
<P> Embedded commands: <BR><BR>

<CODE> &lt;!--#exec cgi="/cgi-bin/relocate.pl" --&gt; <BR>
</CODE>
</P>

<P> Result: <BR>  <!--#exec cgi="/cgi-bin/relocate.pl" --> </P>
</BODY>
</HTML>
```
```

In the listing, the only SSI call in the file is:

```
```
<!--#exec cgi="/cgi-bin/relocate.pl" -->
```
```

The output of this is an HTML anchor, as shown in Figure 13-4.

![](bbox=[0.18, 0.49, 0.71, 0.68])

**Figure 13-4: Output of the `exec_cg12.shtml` file**

# cmd

When calling a program other than a CGI program, you can use the `cmd` version of the `exec` call. The server executes the given string using the `sh` shell (`/bin/sh` on most Unix systems. The Include variables are available to this command. For example, Listing 13-6 shows a file called `exec_cmd.shtml`.

# Listing 13-6: `exec_cmd.shtml`

```
```
<HTML>
<HEAD> <TITLE> Apache Server 2 - Chapter 13 </TITLE></HEAD>
<BODY BGCOLOR="white">
```
```