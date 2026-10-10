
Return the number of elements in the source array *s*. The behavior is the same as that of **asort()**, except that the array *indices* are used for sorting, not the array values. When done, the array is indexed numerically, and the values are those of the original indices. The original values are lost; thus provide a second array if you wish to preserve the original. The purpose of the optional string *how* is the same as described in **asort()** above.

### **gensub**(*r*, *s*, *h* [$_{,} *t*])

Search the target string *t* for matches of the regular expression *r*. If *h* is a string beginning with **g** or **G**, then replace all matches of *r* with *s*. Otherwise, *h* is a number indicating which match of *r* to replace. If *t* is not supplied, use **$0** instead. Within the replacement text *s*, the sequence **\n**, where *n* is a digit from 1 to 9, may be used to indicate just the text that matched the *n*’th parenthesized subexpression. The sequence **\0** represents the entire matched text, as does the character **&**. Unlike **sub()** and **gsub()**, the modified string is returned as the result of the function, and the original target string is *not* changed.

### **gsub**(*r*, *s* [$_{,} *t*])

For each substring matching the regular expression *r* in the string *t*, substitute the string *s*, and return the number of substitutions. If *t* is not supplied, use **$0**. An **&** in the replacement text is replaced with the text that was actually matched. Use **\&** to get a literal **&**. (This must be typed as **\&**; see *GAWK: Effective AWK Programming* for a fuller discussion of the rules for **&**’s and backslashes in the replacement text of **sub()**, **gsub()**, and **gensub()**.)

### **index**(*s*, *t*)

Return the index of the string *t* in the string *s*, or 0 if *t* is not present. (This implies that character indices start at one.) It is a fatal error to use a regexp constant for *t*.

### **length**([*s*])

Return the length of the string *s*, or the length of **$0** if *s* is not supplied. As a non-standard extension, with an array argument, **length()** returns the number of elements in the array.

### **match**(*s*, *r* [$_{,} *a*])

Return the position in *s* where the regular expression *r* occurs, or 0 if *r* is not present, and set the values of **RSTART** and **RLENGTH**. Note that the argument order is the same as for the **~** operator: *str* ~ *re*. If array *a* is provided, *a* is cleared and then elements 1 through *n* are filled with the portions of *s* that match the corresponding parenthesized subexpression in *r*. The 0th element of *a* contains the portion of *s* matched by the entire regular expression *r*. Subscripts **a[n, “start”]**, and **a[n, “length”]** provide the starting index in the string and length respectively, of each matching substring.

### **split**([*s*, *a* [$_{,} *r* [$_{,} *seps*]]])

Split the string *s* into the array *a* and the separators array *seps* on the regular expression *r*, and return the number of fields. Element values are the portions of *s* that matched *r*. The value of **seps[i]** is the separator that appeared in front of **a[i+1]**. If *r* is omitted, **FPAT** is used instead. The arrays *a* and *seps* are cleared first. Splitting behaves identically to field splitting with **FPAT**, described above.

### **split**(*s, a [r [, seps]]*)

Split the string *s* into the array *a* and the separators array *seps* on the regular expression *r*, and return the number of fields. If *r* is omitted, **FS** is used instead. The arrays *a* and *seps* are cleared first. **seps[i]** is the field separator matched by *r* between **a[i]** and **a[i+1]**. If *r* is a single space, then leading whitespace in *s* goes into the extra array element **seps[0]** and trailing whitespace goes into the extra array element **seps[n]**, where *n* is the return value of **split**(*s, a, r, seps*). Splitting behaves identically to field splitting, described above.

### **sprintf**(*fmt, expr-list*)

Print *expr-list* according to *fmt*, and return the resulting string.

### **strtonum**(*str*)

Examine *str*, and return its numeric value. If *str* begins with a leading **0**, treat it as an octal number. If *str* begins with a leading **0x** or **0X**, treat it as a hexadecimal number. Otherwise, assume it is a decimal number.

### **sub**(*r, s [, t]*)

Just like **gsub**(*), but replace only the first matching substring.

### **substr**(*s, i [, n]*)

Return the at most *n*-character substring of *s* starting at *i*. If *n* is omitted, use the rest of *s*.

### **tolower**(*str*)

Return a copy of the string *str*, with all the uppercase characters in *str* translated to their corresponding lowercase counterparts. Non-alphabetic characters are left unchanged.

### **toupper**(*str*)

Return a copy of the string *str*, with all the lowercase characters in *str* translated to their corresponding uppercase counterparts. Non-alphabetic characters are left unchanged.

*Gawk* is multibyte aware. This means that **index()**, **length()**, **substr()** and **match()** all work in terms of characters, not bytes.

## Time Functions

Since one of the primary uses of *awk* programs is processing log files that contain time stamp information, *gawk* provides the following functions for obtaining time stamps and formatting them.

### **mktime**(*datespec*)

Turn *datespec* into a time stamp of the same form as returned by **systime()**, and return the result. The *datespec* is a string of the form YYYY MM DD HH MM SS[*DST*]. The contents of the string are six or seven numbers representing respectively the full year including century, the month from 1 to 12, the day of the month from 1 to 31, the hour of the day from 0 to 23, the minute from 0 to 59, the second from 0 to 60, and an optional daylight saving flag. The values of these numbers need not be within the ranges specified; for example, an hour of -1 means 1 hour before midnight.

The origin-zero Gregorian calendar is assumed, with year 0 preceding year 1 and year -1 preceding year 0. The time is assumed to be in the local timezone. If the daylight saving flag is positive, the time is assumed to be daylight saving time; if zero, the time is assumed to be standard time; and if negative (the default), **mktime()** attempts to determine whether daylight saving time is in effect for the specified time. If *datespec* does not contain enough elements or if the resulting time is out of range, **mktime()** returns -1.

### **strftime([{*format* [, *timestamp*], *utc-flag*]})**

Format *timestamp* according to the specification in *format*. If *utc-flag* is present and is non-zero or non-null, the result is in UTC, otherwise the result is in local time. The *timestamp* should be of the same form as returned by **systime()**. If *timestamp* is missing, the current time of day is used. If *format* is missing, a default format equivalent to the output of *date*(1) is used. The default format is available in **PROCINFO["strftime"]**. See the specification for the **strftime()** function in ISO C for the format conversions that are guaranteed to be available.

### **systime()**

Return the current time of day as the number of seconds since the Epoch (1970-01-01 00:00:00 UTC on POSIX systems).

## Bit Manipulation Functions

*Gawk* supplies the following bit manipulation functions. They work by converting double-precision floating point values to **uintmax_t** integers, doing the operation, and then converting the result back to floating point. The functions are:

### **and(v1, v2 [, ...])**

Return the bitwise AND of the values provided in the argument list. There must be at least two.

### **compl(val)**

Return the bitwise complement of *val*.

### **lshift(val, count)**

Return the value of *val*, shifted left by *count* bits.

### **or(v1, v2 [, ...])**

Return the bitwise OR of the values provided in the argument list. There must be at least two.

### **rshift(val, count)**

Return the value of *val*, shifted right by *count* bits.

### **xor(v1, v2 [, ...])**

Return the bitwise XOR of the values provided in the argument list. There must be at least two.
