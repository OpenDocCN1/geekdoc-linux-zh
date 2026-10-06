# Part III Advanced Shell Scripting

# Built-in variables

The awk program uses built-in variables to reference specific features within the program data. This section describes the built-in variables available for you to use in your awk programs and demonstrates how to use them.

# The field and record separator variables

Chapter 16 demonstrated one type of built-in variable available in awk, the data field variables. The data field variables allow you to reference individual data fields within a data record using a dollar sign and the numerical position of the data field in the record. Thus, to reference the first field in the record, you use the $1 variable. To reference the second data field, you use the $2 variable, and so on.

Data fields are delineated by a field separator. By default the field separator character is a whitespace character, such as a space or a tab. Chapter 16 showed how to change the field separator character either on the command line by using the -F command line parameter or within the awk program by using the FS built-in variable.

The FS built-in variable belongs to a group of built-in variables that control how awk handles fields and records in both input and output data. Table 19-1 lists the built-in variables contained in this group.

The FS and OFS variables define how your awk program handles data fields in the data stream. You've already seen how to use the FS variable to define what character separates data fields in a record. The OFS variable performs the same function for the output by using the print command.

By default, awk sets the OFS variable to a space, so when you use the command:

```
print $1,$2,$3
```

### The awk Data Field and Record Variables
| Variable | Description |
| --- | --- |
| FIELDWIDTHS | A space separated list of numbers defining the exact width (in spaces) of each data field. |
| FS | Input field separator character. |
| RS | Input record separator character. |
| OFS | Output field separator character. |
| ORS | Output record separator character. |