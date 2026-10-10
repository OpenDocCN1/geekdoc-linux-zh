# **WARNING**

For test conditions, the only numbers the Bash shell can handle are integers. Although you can use floating-point values for commands, such as `echo`, they will not work properly in test conditions.

# Using string comparisons

Test conditions also allow you to perform comparisons on string values. Performing comparisons on strings can get tricky, as you’ll see. Table 12-2 shows the comparison functions you can use to evaluate two string values.

# TABLE 12-2 The test String Comparisons

| Comparison | Description |
| :--- | :--- |
| `str1 = str2` | Checks if `str1` is the same as string `str2`. |
| `str1 != str2` | Checks if `str1` is not the same as `str2`. |
| `str1 < str2` | Checks if `str1` is less than `str2`. |
| `str1 > str2` | Checks if `str1` is greater than `str2`. |
| `-n str1` | Checks if `str1` has a length greater than zero. |
| `-z str1` | Checks if `str1` has a length of zero. |

The following sections describe the different string comparisons available.

# Looking at string equality

The equal and not equal conditions are fairly self-explanatory with strings. It’s pretty easy to know whether two string values are the same or not:

```
```
$ cat string_test.sh
#!/bin/bash
# Using string test evaluations
```
```