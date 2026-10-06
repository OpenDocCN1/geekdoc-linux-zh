The gawk program uses data field variables to reference data elements within each record.
Table B-3 describes these variables.

# TABLE B-3

# The gawk Data Field and Record Variables

| Variable | Description |
|---|---|
| $0 | The entire record. |
| $1 | The first data field in the record. |
| $2 | The second data field in the record. |
| $n | The nth data field in the record. |
| FIELDWIDTHTHS | A spaced list of numbers defining the exact width (in spaces) of each data field. |
| FS | Input field separator character. |
| RS | Input record separator character. |
| OFS | Output field separator character. |
| ORS | Output record separator character. |

Besides the field and record separator variables, gawk provides some other built-in variables to help you know what's going on with your data and extract information from the shell environment. Table B-4 shows the other built-in variables in gawk.

You can use the built-in variables anywhere in the gawk program script, including the BEGIN and END sections.

# Assigning variables in scripts

Assigning values to variables in gawk programs is similar to how you do it in a shell script, using an assignment statement:

```
$ gawk '
BEGIN{
  testing="This is a test"
  print testing
}'
```

This is a test.

$ Once you assign a value to a variable, you can use that variable anywhere in your gawk script.