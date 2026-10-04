
# DTML AND BUILT-IN ATTRIBUTES

## A.1 The var Tag

The following table lists all var attributes along with examples and corresponding screen output. Attributes marked with an asterisk (*) require at least one argument. This is a more complete version of information presented in Table 4.1.

### Attributes for the var Tag

| Attribute | Function | Example | Output |
| --- | --- | --- | --- |
| name* | See "The name Attribute" in Table 4.1. | | |
| expr* | See "The expr Attribute" in Table 4.1. | | |
| fmt* | See "The fmt Attribute" in Table 4.1. | | |
| null | Defines a string that will be output instead of the value "null." If the value for null is omitted, no text is inserted. | null="The result" returns an empty list. | The result returns an empty list. |

### Attributes for the var Tag (continued)

| Attribute | Function | Output |
| --- | --- | --- |
| missing | Defines a string to be inserted if the variable referred to by name is not in the namespace. If the value for missing is omitted, no text is inserted. | missing="Not found" | Not found |
| lower | Changes all letters to lowercase. | title_id_lower | testpage |
| upper | Converts all letters to uppercase. | title_id_upper | TESTPAGE |
| capitalize | Capitalizes the first letter. | AUTHENTICATED_USER capitalize | Manager |
| specify | Converts the underscore character [] into white space. | id specify (id="index_html") | index html |
| thousands_comma | Inserts commas into character strings that consist solely of numbers at the thousand position. | teststring thousands_comma (teststring="12000") | 12,000 |
| html_quote | Characters significant in HTML are replaced with appropriate HTML entities. | teststring html_quote (teststring="<") | &lt; |
| url_quote | Characters not legal in URLs are properly escaped for insertion into href values. | teststring url_quote (teststring="<") | %3c |
| url_quote_plus | Functions like url_quote, but spaces are converted to plus signs (+) for insertion into href URL CGI queries. | teststring url_quote_plus teststring="two words" | two+words |
| sql_quote | Characters significant to SQL, such as single quotes, are properly escaped (important for SQL methods). | Teststring sql_quote (teststring="How're you?") | How're you |

### Attributes for the var Tag (continued)

| Attribute | Function | Example | Output |
|---|---|---|--|
| newline_to_br | Inserts an HTML line break tag <br> in the source code at each new line in the string value. | teststring_newline_to_br (teststring="Hello\nYou") | Hello<br>You |
| size | Displays only the specified number of characters from a string. | teststring size=6 (teststring="How're you?") | Haw're... |
| else | Specifies a string that is inserted instead of omitted characters (used with size). | teststring size=6 etc="--" (teststring="How're you?") | How're - |

## Standard fmt Attribute Formats

| Name | Description |
|---|---|--|
| AMPM | Returns the time including seconds. |
| AMMinutes | Returns the time without seconds. |
| aCommon | The time is displayed in the format Mar 1, 2002 1:45 pm. |
| aCommonZ | The time is displayed in the format Mar 1, 2002 1:45 pm US/Eastern. |
| aDay | Returns the abbreviated name of the day of the week. |
| aMonth | Returns the name of the month. |
| ampm | Returns the suffix am or pm. |
| Date | Returns the date string for an object. |
| Day | Returns the full name of the day of the week. |
| DayOfWeek | Same as Day: Returns the full name of the day of the week. |
| day | Returns the day as a number. |
| dayOfYear | Returns the day of the year in the context of the time zone for the object. |
| dd | Returns the day as a two-digit string. |
| fCommon | The time is displayed as March 1, 1997 1:45 pm. |
| fCommonZ | The time is displayed as March 1, 1997 1:45 pm US/Eastern. |
| h_12 | Returns the time in 12-hour mode. |
| h_24 | Returns the time in 24-hour mode. |

### Standard fmt Attribute Formats (continued)

| Name | Description |
| --- | --- |
| hour | Returns the time in 24-hour mode. |
| isCurrentHour | Returns as True if the object Date/Time is the same as the current time (in the context of the time zone display of the object). |
| isCurrentMonth | Returns as True if the object Date/Time is in the current month (in the context of the time zone display of the object). |
| isFuture | Returns as True if the object Date/Time is in the future. |
| isLeapYear | Returns as True if the current year (in the time zone of the object) is a leap year. |
| isPast | Returns as True if the object Date/Time is in the past. |
| Mon_ | Returns the full name of the month. |
| Mon | Same as aMonth: Returns the abbreviated name of month. |
| Manth | Returns the full name of the month. |
| minute | Returns the minutes. |
| mm | Returns the month as a two-digit string. |
| month | Returns the month as a number. |
| natEqualTo(t) | Compares the DateTime object with another DateTime object with a decimal number, such as those returned by the time module. |
| PreciseAMPM | Returns the timestring for the object. |
| PreciseTime | Returns the timestring for the object. |
| pCommon | The time is displayed as Mar 1, 2002 1:45 pm. |
| pCommonZ | The time is displayed as Mar 1, 2002 1:45 pm US/Eastern. |
| pDay | Returns the day abbreviated with a period. |
| pMonth | Returns the month abbreviated with a period. |
| rfc822 | Returns the date in RFC822 format (the format used in HTTP headers). |
| second | Returns the seconds. |
| TimeMinutes | Returns the timestring for the object without seconds. |
| Time | Returns the timestring for the object with seconds. |
| timezone | Returns the time zone in which the object is displayed. |
| year | Returns the object's calendar year. |
| yy | Returns the calendar year as a two-digit number. |

## A.1.1 Special Formats

These special formats can be used with fmt attribute on other data types.

| Special Format | Description |
| --- | --- |
| whole-dollars | Displays a numeric value with the dollar sign. |
| dollars-and-cents | Displays a numeric value with the dollar sign and two decimal places. |
| collection-length | Returns the length of a collection of objects. |
| structured-text | Renders the value as structured text, which generates HTML text data. |

### C-Style Formats for the fmt Attribute

| Code | Description | Example | Result |
| --- | --- | --- | --- |
| d | Decimal numbers with preceding sign | fmt="%.3d" | -020 |
| e | Scientific notation | fmt="%.3e" | -2.000E+001 |
| E | Scientific notation | fmt="%.3E" | -2.000E+001 |
| f | Real decimal numbers | fmt="%.3f" | -20.000 |
| g | e or f abbreviated | fmt="%.3g" | -20 |
| G | E or F abbreviated | fmt="%.3G" | -20 |
| i | Decimal numbers with preceding sign | fmt="%.3i" | -020 |
| o | Octals without preceding sign | fmt="%.3o" | 3777777754 |
| s | Character string | fmt="%.2s" | -2 |
| u | Decimal numbers without preceding sign | fmt="%.3u" | 4294967276 |
| x | Hexadecimal numbers with lowercase letters and without preceding sign | fmt="%.3x" | ffec |
| X | Hexadecimal numbers with uppercase letters and without preceding sign | fmt="%.3X" | FFFFFEC |

## A.2 The Namespace Variable

### Namespace Attribute Variables

| Attribute | Function | Example | Output |
|---|---|---|---|
| abs(number) | Calculates the absolute value of a number. | _.abs(-3) | 3 |
| chr(number) | Returns the character associated with a numeric ASCII value. | _.chr(97) | a |
| divmod(number 1, number 2) | Calculates the whole quotient and the whole remainder when dividing two numbers. | _.divmod(20, 3) _.divmod(12, 3) | (6, 2) (4, 0) |
| float(number) | Converts a value to a floating point number. | _.float(4) | 4.0 |
| getitem(name,call]) | Looks up a name in the namespace (frame instance, [...]), but also takes an optional argument that determines if the returned object should be called. If the argument is omitted, the object is not called, which is the opposite of the behavior of [...]. | _.getitem('some_name') | Content of some_name |
| hash(object) | Returns the hash value of an object. | _.hash(index.html) | 504824376 |
| hex(number) | Converts a number into hexadecimal. | _.hex(5) _.hex(8) | 0x5 0x10 |
| int(number) | Converts a value to an integer. Any decimal values are truncated, and no rounding occurs. | _.int(4.25) _.int('4.85') | 4 4 |
| len(seq) | Calculates the number of elements in a sequence. | _.len('Hello') _.len(['I', 'You']) | 5 2 |
| max(seq) | Outputs the largest element in a list. | _.max([1, '3', '4', '5']) _.max(['Ah', 'You']) | 5 Yau |
