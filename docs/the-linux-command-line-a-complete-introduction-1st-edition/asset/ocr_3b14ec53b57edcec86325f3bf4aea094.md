# Table 21-5 (continued)

| Component | Description |
|---|---|
| *width* | A number specifying the minimum field width |
| *.precision* | For floating-point numbers, specify the number of digits of precision to be output after the decimal point. For string conversion, *precision* specifies the number of characters to output. |

Table 21-6 lists some examples of different formats in action.

# Table 21-6: print Conversion Specification Examples

| Argument | Format | Result | Notes |
|---|---|---|---|
| 380 | "%d" | 380 | Simple formatting of an integer |
| 380 | "%#x" | 0x17c | Integer formatted as a hexadecimal number using the alternate format flag |
| 380 | "%05d" | 00380 | Integer formatted with leading zeros (padding) and a minimum field width of five characters |
| 380 | "%05.5f" | 380.00000 | Number formatted as a floating-point number with padding and 5 decimal places of precision. Since the specified minimum field width (5) is less than the actual width of the formatted number, the padding has no effect. |
| 380 | "%010.5f" | 0380.00000 | Increasing the minimum field width to 10 makes the padding visible. |
| 380 | "%+d" | +380 | The + flag signs a positive number. |
| 380 | "%-d" | 380 | The - flag left-aligns the formatting. |
| abcdefghijk | "%5s" | abcdefghijk | A string is formatted with a minimum field width. |
| abcdefghijk | "%.5s" | abcde | By applying precision to a string, it is truncated. |