```
```
> for (test in var)
>     print "Index:"test," - Value:";var[test]
> }
Index: a - Value: 1
Index: g - Value: 2
---
Index: a - Value: 1
$    
```
```

Once you delete an index value from the associative array, you can't retrieve it.

# ## Considering Patterns

The *gawk* program supports several types of matching patterns to filter data records, in much the same way as the *sed* editor. Chapter 19 already showed two special patterns in action. The *BEGIN* and *END* keywords are special patterns that execute statements before or after the data stream data has been read. Similarly, you can create other patterns to execute statements when matching data appears in the data stream.

This section demonstrates how to use matching patterns in your *gawk* scripts to limit what records a program script applies to.

# ### Regular expressions

Chapter 20, "Regular Expressions," showed how to use regular expressions as matching patterns. You can use either a basic regular expression (BRE) or an extended regular expression (ERE) to filter which lines in the data stream the program script applies to.

When you're using a regular expression, it must appear before the left brace of the program script that it controls:

```
```
$ gawk '/BEGIN{PS=""} /11/{print $1}' data1
data11
$
```
```

The regular expression /11/ matches records that contain the string 11 anywhere in the data fields. The *gawk* program matches the defined regular expression against all of the data fields in the record, including the field separator character:

```
```
$ gawk '/BEGIN{PS=""} ,/[{print $1}] data1
data11
data21
data31
$
```
```

This example matches the comma used as the field separator in the regular expression. This is not always a good thing. It can lead to problems trying to match data specific to one data field that may also appear in another data field. If you need to match a regular expression to a specific data instance, you should use the matching operator.