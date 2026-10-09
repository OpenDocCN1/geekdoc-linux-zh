# Using SSI Commands

SSI commands are embedded in HTML pages in the form of comments. The base command structure looks like this:

```
<!--#command argument1=value argument2=value argument3=value -->
```

The value is often enclosed in double quotes; many commands only allow a single attribute-value pair. Note that the comment terminator --> should be preceded by white space to ensure that it isn't considered part of the SSI command.

The following sections examine all the available SSI commands.

# config

The `config` command enables you to configure the `parse error` message that appear, as well as the formatting that is used for displaying time and file size information. This is accomplished with the following lines of code:

```
config errmsg="error message"
config sizefmt=["bytes" | "abbrev"]
config timefmt=format string
```

`config errmsg="error message"` shows you how to create a custom error message, which is displayed when a parsing error occurs. For example, Listing 13-1 shows a file called `config_errmsg.shtml`.

# Listing 13-1: config_errmsg.shtml

```
<HTML>
<BODY>
<TITLE> Apache Server 2 - Chapter 13 </TITLE>
</HEAD>

<BODY BGCOLOR="white">

<FONT SIZE=+1 FACE="Arial"> Simple SSI Example #1</FONT>
<HR SIZE=1>

<P> Example of the SSI <STRONG>config errmsg</STRONG> command:
</P> Embedded commands: <BR><BR>

<CODE>
&lt;!--#config errmsg="SSI error! Please notify the webmaster." -&gt; <BR>
&lt;!--#config badcommand="whatever" -&gt;
```