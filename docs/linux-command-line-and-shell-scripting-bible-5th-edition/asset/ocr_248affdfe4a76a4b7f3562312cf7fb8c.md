The gawk program executes the code in the BEGIN section first, then processes any data in the input stream, and then executes the code in the END section.

# The gawk variables

The gawk program is more than just an editor; it's a complete programming environment. As such, lots of commands and features are associated with gawk. This section shows the main features you need to know for programming with gawk.

# Using the built-in variables

The gawk program uses built-in variables to reference specific features within the program data. This section describes the gawk built-in variables available for you to use in your gawk programs and demonstrates how to use them.

The gawk program defines data as records and data fields. A record is a line of data (delineated by the newline characters by default), and a data field is a separate data element within the line (delineated by a whitespace character, such as a space or tab, by default).

The gawk program uses data field variables to reference data elements within each record. Table B.3 describes these variables.

TABLE B.3 The gawk Data Field and Record Variables
| Variable | Description |
| :------- | :---------- |
| $0 | The entire data record |
| $1 | The first data field in the record |
| $2 | The second data field in the record |
| $n | The nth data field in the record |
| FIELDWIDTHS | A space-separated list of numbers defining the exact width (in spaces) of each data field |
| FS | Input field separator character |
| RS | Input record separator character |
| OFS | Output field separator character |
| ORS | Output record separator character |

In addition to the field and record separator variables, gawk provides some other built-in variables to help you know what's going on with your data and to extract information from the shell environment. Table B.4 shows the other built-in variables in gawk.