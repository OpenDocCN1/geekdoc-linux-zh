As you can see, the variable name is prefixed by a $ sign. Here's another example:

```
<!--#config errmsg="An error occurred in $DOCUMENT_NAME page." -->
```

When using variables in a `var="variable"` field, the $ sign is not necessary. For example:

```
<!--#echo var="DOCUMENT_NAME" -->
```

> If you need to insert a literal dollar sign into the value of a variable, you can insert the dollar sign using backslash quoting. For example:

```
<!--#set var="password" value="\$cheese" -->  <!--#echo var="password" -->
```

This prints `$cheese` as the value of the variable `"password"`.

Also, if you need to reference a variable name in the middle of a character sequence that might otherwise be considered a valid identifier on its own, use a pair of braces around the variable name. For example:

```
<!--#set var="uniqeid" value="${DATE_LOCAL}_${REMOTE_HOST}" -->
```

This sets `uniqeid` to something similar to `Saturday, 17-Mar-2001 13:02:47 PST_207.183.233.19`, depending on the `timefmt` setting and the IP address of the Web client.

# # Flow Control Commands

Like many programming languages, program flow control is also available in the SSI module. By using flow control commands, you can conditionally create different output. The simplest flow control (that is, conditional) statement is:

```
<!--#if expr="test_expression" -->  <!--#endif -->
```

Here, the `test_expression` is evaluated, and if the result is true, then all the text up to the `endif` command is included in the output. The `test_expression` can be a *string*, which is true if the string is not empty, or an expression comparing values of two strings.

The comparison operators allowed are `=`, `!=`, `<`, `>`, `<=`, or `>=`. A generic form of such an SSI statement looks as follows:

```
<!--#if expr="string1 operator string2" -->  <!--#endif -->
```