| Argument | Format | Result | Notes |
|---|---|---|---|
| 380 | "%#x" | 0x17c | Integer formatted as a hexadecimal number using the “alternate format” flag. |
| 380 | "%05d" | 00380 | Integer formatted with leading zeros (padding) and a minimum field width of five characters. |
| 380 | "%05.5f" | 380.00000 | Number formatted as a floating-point number with padding and five decimal places of precision. Since the specified minimum field width (5) is less than the actual width of the formatted number, the padding has no effect. |
| 380 | "%010.5f" | 0380.00000 | By increasing the minimum field width to 10, the padding is now visible. |
| 380 | "%+d" | +380 | The + flag signs a positive number. |
| 380 | "%-d" | 380 | The - flag left-aligns the formatting. |
| abcdefghijk | "%5s" | abcdefghijk | A string formatted with a minimum field width. |
| abcdefghijk | "%.5s" | abcde | By applying precision to a string, it is truncated. |

Again, printf is used mostly in scripts where it is employed to format tabular data, rather than on the command line directly. But we can still show how it can be used to solve various formatting problems. First, let's output some fields separated by tab characters.

```
[me@linuxbox ~]$ printf "%s\t%s\t%s\n" str1 str2 str3
str1    str2    str3
```

By inserting \t (the escape sequence for a tab), we achieve the desired effect. Next, here are some numbers with neat formatting: