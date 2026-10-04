# Table 4-2: Standard fmt Attribute Formats (continued)

| Name | Description |
| --- | --- |
| timezone | Returns the time zone in which the object is displayed. |
| year | Returns the object's calendar year. |

# Table 4-3: Special Formats that Can Be Used with the fmt Attribute

| Special Format | Description |
| --- | --- |
| whole-dollars | Displays a numeric value with the dollar sign. |
| dollars-and-cents | Displays a numeric value with the dollar sign and two decimal places. |
| collection-length | Returns the length of a collection of objects. |
| structured-text | Renders the value as structured text, which generates HTML from Zope structured text data. |

#  4.3.2 The Namespace Variable

Using the namespace variable, you can refer to variables within expressions that are not valid variables in Python, including

+   * Names that do not begin with a letter
* Names that contain characters significant in expressions such as the dash (-), period (.), equals sign (=), and so on.

> The second rule shows why it is inconvenient to have periods in object names. The main reason Zope uses the variable name index_html instead of index.html: index.html is not usable as a variable in expressions.

The namespace variable is the underscore (_) character. To directly refer to something, enclose the variable name in quotation marks and square brackets, as shown below. (Because this expression must be evaluated, make sure you use double quotation marks.)

```
<html-var exp="[sequence-number] / 5">
```

This example refers to a variable in our namespace named "sequence-number" (which is generally created by the dm-in tag, discussed in Section 4.3.10). Because this variable contains a dash character (-), which means "subtract" in an expression, we must use the underscore variable to look it up here. If we did not, the expression would be incorrectly interpreted to mean "sequence minus number divided by 5"—that is, sequence - number / 5.

# 4.3.2.1 Using the Namespace Variable for Indirect Namespace Lookups

The underscore variable can also be used to look up names in the namespace that themselves are stored as variable data, a process called indirection. Indirection