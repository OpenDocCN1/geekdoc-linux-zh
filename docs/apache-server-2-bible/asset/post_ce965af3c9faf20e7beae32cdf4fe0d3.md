
### printenv

`<!--#printenv -->`

prints all the Include and CGI environment variables available. To make the output more readable, use of the `<PRE>` tag pair is recommended.

### set

The `set` command sets the value of a user-defined variable. The syntax is:

```
set var="variable name" value="value of the variable"
```

For example:

```
<!--#set var="home" value="index.shtml" -->
```

## SSI Variables

The SSI module makes a set of variables, in addition to the CGI environment variables (see Chapter 12), available to all SSI files. These variables are called the `include` variables. These can be used by SSI commands (`echo`, `if`, `elif`, and so on) and by any program invoked by an SSI command. The `include` variables are listed in Table 13-2.

| Variable | Meaning |
| :--- | :--- |
| DATE_GMT | The current date in Greenwich Mean Time. |
| DATE_LOCAL | The current date in the local time zone. |
| DOCUMENT_NAME | The current SSI filename. |
| DOCUMENT_URI | The (%-decoded) URL path of the document. |
| LAST_MODIFIED | The last modification date of the current file. The date is subject to the config command's timefmt format. |

The `include` variables and the CGI variables are preset and available for use. Any of the variables that are preset can be used as arguments for other commands. The syntax for using defined variables is:

```
<!--#command argument1="$variable1" argument2="$variable2" ...-->
```

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

## Flow Control Commands

Like many programming languages, program flow control is also available in the SSI module. By using flow control commands, you can conditionally create different output. The simplest flow control (that is, conditional) statement is:

```
<!--#if expr="test_expression" -->  <!--#endif -->
```

Here, the `test_expression` is evaluated, and if the result is true, then all the text up to the `endif` command is included in the output. The `test_expression` can be a *string*, which is true if the string is not empty, or an expression comparing values of two strings.

The comparison operators allowed are `=`, `!=`, `<`, `>`, `<=`, or `>=`. A generic form of such an SSI statement looks as follows:

```
<!--#if expr="string1 operator string2" -->  <!--#endif -->
```

Note that *string2* can be a regular expression in the `/regular expression patterns/` form. See Appendix B for details on regular expressions.

Let’s look at an example of a string by itself:

```
<!--#if expr="foobar" -->
This test is always successful.
<!--#endif -->
```

This syntax always prints *This test is successful*. because the expression is *true* when the *test_expression* is not an empty string. If *expr*="*foobar*" is changed to *expr*=""* or *expr*="'*'*, however, then the text within the `if-endif` block will never be part of the output.

Now let’s look at an example of a string equality test:

```
<!--#set var="quicksearch" value="yes" -->
<!--#if expr="$quicksearch = yes" -->

Quick search is requested.
<!--#endif -->
```

Here, the *variable* called *quicksearch* is *being set* with the *value yes*, and is later being compared with *yes*. Because the *set value* and *comparison value* are *equal*, the *Quick search is requested* line will be the output.

Using *logical operators* such as `!`, `&`, and `||`, you can create more complex *test_expressions*. For *example*:

```
<!--#if expr="${REMOTE_ADDR} = /207.183.233/
&& ${DOCUMENT_NAME} = /timesheet/" -->
<!--#include virtual="/cgi-bin/timecard.pl" -->
<!--#endif -->
```

Here, the *test_expression* is composed of two smaller *expressions*. The *first subexpression*, `${REMOTE_ADDR} = /207.183.233/`, is *evaluated* to *determine whether the server-defined variable* *REMOTE_ADDR* *matches the 207.183.233 network address*. Note that the address is written using the *simple regular expression* `/207.183.233/`, where each *`\.`* (*period*) is *escaped using a \ (backslash) character*. This was *necessary to undo the `\.` character’s special meaning* in regular *expressions*. See *Appendix C* for more *details* on *regular expressions*.

The *second subexpression*, `${DOCUMENT_NAME} = /timesheet/`, is *evaluated to determine whether the current SSI file being processed has a name that* matches the string `timesheet`. And, finally, the `&&` (logical AND) requires that both subexpressions be true for the entire expression to be true. If the final expression is true, then the `/cgi-bin/timecard.pl` script is run using the `include virtual` command.

Other logical operations that you can perform on the `test_expression` are:

```
<!--#if expr="! test_expression" -->  
This is printed only when the test_expression is false.  
<!--#endif -->
```

and

```
<!--#if expr="test_expression1 || test_expression2" -->  
This is printed when at least one of the test_expressions is  
true.  
<!--#endif -->
```

The `=` (equal) and `!=` (not equal) operators have higher precedence than the `&&` (and) and the `||` (or) operators. The `!` (not) operator has the highest priority. You can use a pair of parentheses to increase priority. For example:

```
<!--#if expr="($win = yes && $loss = false) != ($profit = yes)" -->
```

Here, the `($win = yes && $loss = false)` is evaluated before the `!=` operator is evaluated.

Anything that is not recognized as a variable or as an operator is treated as a string. Strings can also be quoted, like this: `'string'`. Unquoted strings cannot contain white space (blanks and tabs) because they are used to separate tokens such as variables. If multiple strings are found in a row, they are concatenated using blanks.

If you require more complex flow control constructs, you can use the following:

```
<!--#if expr="test_condition1" -->

    Do something specific to the first test condition.

<!--#elif expr="test_condition2" -->

    Do something specific to the second condition.

<!--#else -->

    Do something as default.

<!--#endif -->
```

The `elif` enables you to create an `else-if` condition. For example:

```
<!--#if expr="$[HTTP_USER_AGENT] = /MSIE/" -->
  <!--#set var="browser" value="MicrosoftIE" -->
  <!--#include file="mypage.asp" -->

<!--#else -->
  <!--#set var="browser" value="Others" -->
  <!--#include file="mypage.html" -->

<!--#endif -->
```

Here, the `HTTP_USER_AGENT` variable is checked to determine whether it contains the string `MSIE` (a string used by Microsoft Internet Explorer browser). If it does contain this string, then the browser variable is set to `MicrosoftIE`, and a file named `mypage.asp` is inserted in the current document. On the other hand, if the `HTTP_USER_AGENT` does not contain the `MSIE` string, it is assumed to be the another browser (such as Netscape Navigator, Lynx), and thus the browser variable is set to `Others` and the `mypage.html` file is inserted in the current document. By using the `if-then-else` construct, this example sets a different value to the same variable and loads different files.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_427_0.png)
