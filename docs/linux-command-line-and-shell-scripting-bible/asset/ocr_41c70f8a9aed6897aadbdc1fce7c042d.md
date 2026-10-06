```
data21
data31
$
```

This example matches the comma as the field separator in the regular expression. This is not
always a good thing. It can lead to trying to match data specific to one data field that
may appear in another data field. If you need to match a regular expression to a specific data
instance, you should use the matching operator.

# The matching operator

The matching operator allows you to restrict a regular expression to a specific data field in
the records. The matching operator is the tilde symbol (~). You specify the matching operator, along
with the data field variable, and the regular expression to match.

```
$1 ~ /data/
```

The $1 represents the first data field in the record. This expression filters records where
the first data field starts with the text data. Here's an example of using it in a gawk program
script:

The matching operator compares the second data field with the regular expression /data2/,
which indicates the string starts with the text data2.

This is a powerful tool that is commonly used in gawk program scripts to search for specific data
elements in a data file:

```
$ gawk -F: '$1 ~ /rich/(print $1,$NF)' /etc/passwd
rich /bin/bash
$
```

This example searches the first data field for the text rich. When it finds the pattern in a record,
it prints the first and last data field values of the record.

You can also negate the regular expression by using the ! symbol:

```
$1 ~ /expression/
```

If the regular expression isn't found in the record, the program script is applied to the record
data:

In this example the gawk program script prints the first data field of records where the second
data field doesn't start with the text data2.