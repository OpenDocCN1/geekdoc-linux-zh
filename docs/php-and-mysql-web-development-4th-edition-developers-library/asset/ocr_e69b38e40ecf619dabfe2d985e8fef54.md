governing default values is more complex. See Section 3.2.6.2, “The TIMESTAMP Data Type,” for details.

# 3.2.6.5 Working with Date and Time Values

MySQL tries to interpret input values for date and time columns in a variety of formats, including both string and numeric forms. Table 3.16 shows the allowable formats for each of the date and time types.

Table 3.16 Date and Time Type Input Formats

| **Type** | **Allowable Formats** |
| :--- | :--- |
| DATETIME, TIMESTAMP | ‘CCYY-MM-DD hh:mm:ss’ |

MySQL interprets formats that have no century part (cc) using the rules described in Section 3.2.6.6, “Interpretation of Ambiguous Year Values.” For string formats that include delimiter characters, you don’t have to use ‘-’ for dates and ‘:’ for times. Any punctuation character may be used as the delimiter. Interpretation of values depends on context, not on the delimiter. For example, although times are typically specified using a delimiter of ‘:’, MySQL won’t interpret a value containing ‘:’ as a time in a context where a date is expected. In addition, for the string formats that include delimiters, you need not specify