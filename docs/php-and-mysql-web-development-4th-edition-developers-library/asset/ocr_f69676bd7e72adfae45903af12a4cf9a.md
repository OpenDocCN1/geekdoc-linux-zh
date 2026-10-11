+   * In HTML, tag and attribute names are not case sensitive. For example, `<BODY BGCOLOR="white">` and `<body bgcolor="white">` are the same. In XHTML, tag and attribute names should be lowercase, so only `<body bgcolor="white">` is allowable.
+   * HTML attribute values can be unquoted or even missing. For example, this table data cell construct is legal in HTML:
+     `<td width=40 nowrap>Some text</td>`
+   
+   In XHTML, attributes must have values, and they must be quoted. A common convention for HTML attributes that normally are used without a value is to use the attribute name as its value. The XHTML equivalent of the preceding `<tr>` element looks like this:
+   `<td width="40" nowrap="nowrap">Some text</td>`
+   
+   All the Web scripts in this book generate output that conforms to XHTML rules. In this chapter, we’ll rely on CGI.pm to generate properly formatted XHTML markup. The scripts discussed in Chapter 9 also produce XHTML but generate the markup tags for themselves because PHP doesn’t provide tag-generating functions the way CGI.pm does.

# ### 8.4.2.3 Escaping HTML and URI Text

If text that you write to a Web page may contain special characters, you should make sure that they are escaped properly by processing the text with `escapeHTML()` . This is also true when you construct URLs that may contain special characters, although in that case you should use the `escape()` function instead. It’s important to use the appropriate encoding function because each one recognizes a different set of special characters and encodes them differently. `escapeHTML()` escapes special characters as their equivalent HTML entities. For example, `<` becomes the `&lt;` entity. `escape()` escapes each special character as `%` followed by two hexadecimal digits representing the numeric character code, so `<` becomes `%3C` . Consider the following short Perl script, `escape_demo.pl` , which demonstrates both forms of escaping:

```
#!/usr/bin/perl
# escape_demo.pl – demonstrate CGI.pm output-encoding functions

use strict;
use warnings;
use CGI qw(escapeHTML escape);  # import escapeHTML() and escape()

# Assign default string value, but use command-line argument if present
my $s = '<<2, right">' ;
$s= shift (@ARGV) if @ARGV;
print "Unencoded string:  	", $s, "\n";
print "Encoded for use as HTML text: ", escapeHTML($s), "\n";
print "Encoded for use in a URL:	", escape($s), "\n";
```