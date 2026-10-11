If the value of name_val is something like `O\'Malley, Brian`, the resulting statement is illegal because a quote appears inside a quoted string:

```
SELECT * FROM mytbl WHERE name= `O\'Malley, Brian`
```

You need to treat the inner quote specially so that the server doesn\'t interpret it as the end of the name. The standard SQL convention for doing this is to double the quote within the string. MySQL understands that convention, and also allows the quote to be preceded by a backslash, so you can write the statement using either of the following formats:

```
SELECT * FROM mytbl WHERE name= `O"Malley, Brian` 
SELECT * FROM mytbl WHERE name= `O\"Malley, Brian`
```

To deal with this problem, use `mysql_real_escape_string()`, which encodes special characters to make them usable in quoted strings. Characters that `mysql_real_escape_string()` considers special are the null byte, single quote, double quote, backslash, newline, carriage return, and Control-Z. (The last one is special on Windows, where it often signifies end-of-file.)

When should you use `mysql_real_escape_string()`? The safest answer is \"always.\" However, if you\'re sure of the format of your data and know that it\'s okay—perhaps because you have performed some prior validation check on it—you need not encode it. For example, if you are working with strings that you know represent legal phone numbers consisting entirely of digits and dashes, you don\'t need to call `mysql_real_escape_string()`. Otherwise, you probably should.

`mysql_real_escape_string()` encodes problematic characters by turning them into two-character sequences that begin with a backslash. For example, a null byte becomes `\0`, where the `0` is a printable ASCII zero, not a null. Backslash, single quote, and double quote become `\\`, `\'`, and `\"`.

To use `mysql_real_escape_string()`, invoke it like this:

```
to_len = mysql_real_escape_string( conn, to_str, from_str, from_len);
```

`mysql_real_escape_string()` encodes `from_str` and writes the result into `to_str`. It also adds a terminating null, which is convenient because you can use the resulting string with functions such as `strcpy()`, `strlen()`, or `printf()`.

`from_str` points to a char buffer containing the string to be encoded. This string may contain anything, including binary data. `to_str` points to an existing char buffer where you want the encoded string to be written; do not pass an uninitialized or NULL pointer, expecting `mysql_real_escape_string()` to allocate space for you. The length of the buffer pointed to by `to_str` must be at least (`from_len`+2)+1 bytes long. (It\'s possible that every character in `from_str` will need encoding with two characters; the extra byte is for the terminating null.)

`from_len` and `to_len` are unsigned long values. `from_len` indicates the length of the data in `from_str`; it\'s necessary to provide the length because `from_str` may contain null bytes and cannot be treated as a null-terminated string. `to_len`, the return value from `mysql_real_escape_string()`, is the actual length of the resulting encoded string, not counting the terminating null.