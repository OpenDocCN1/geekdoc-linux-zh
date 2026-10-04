# 10.4 HTML Display Package

After Clicking Top Hypertext Link

![](bbox=[0.237, 0.163, 0.762, 0.246])

Script Output
HMLink_callback was invoked with win: .t href: Text2

# 10.4.3 Extending the html_library package

The 0.3 revision of the html_library.tcl package supports HTML version 2.0. It supports forms, but not tables.

However, the package is designed so you can easily add support for other tags. In this section, we'll add support for a simple table to show how this package can be extended.

The html_library package works by using a set of regular expression statements to turn a hypertext tag into a command to be evaluated. The naming convention for the commands is to merge the HTML tag identifier (converted to lowercase) into the name of a procedure.

```
Syntax: HMtag_htmlTag window param text
```

HMtag_htmlTag
The procedure to invoke when htmlTag is evaluated in the HTML text.

+   - window: The text widget that will receive the text.
- param: Any parameters that may be included with the HTML tag.
- text: The name of the variable that contains the text in the calling procedure. This procedure must use upvar to gain access to the text. The text may be modified in this procedure as necessary before it is inserted into the text window by the calling procedure.