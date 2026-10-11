```
```sql
'abcd'				→ 'abcd'
CONVERT('abcd' USING ucs2)		→ 'abcd'
CHARSET('abcd')			→ 'latin1'
CHARSET(CONVERT('abcd' USING ucs2))	→ 'ucs2'
```
```

Preceding a string with a character set introducer does not cause conversion of the string, but MySQL interprets it as though it has the character set indicated by the introducer:

```
```sql
CHARSET(ucs2 'abcd')		→ 'ucs2'
```
```

To determine the hexadecimal value of the UTF-8 character that corresponds to a given hexadecimal UCS-2 character, combine `CONVERT()` with `HEX()`. The following expression determines the UTF-8 value of the trademark symbol:

```
```sql
HEX(CONVERT(ucs2 0x2122 USING utf8))	→ 'E284A2'
```
```

To change the collation of a string, use the `COLLATE` operator. To check whether the result has the desired collation, use the `COLLATION()` function:

```
```sql
COLLATION('abcd')			→ 'latin1_swedish_ci'
COLLATION('abcd' COLLATE latin1_bin)	→ 'latin1_bin'
```
```

The character set and collation must be compatible. If they are not, use a combination of `CONVERT()` to convert the character set first and `COLLATE` to change the collation:

```
```sql
CONVERT('abcd' USING latin2) COLLATE latin2_bin
```
```

To convert a binary string to a non-binary string that has a given character set, use `CONVERT()`: .

```
```sql
0x61626364			→ 'abcd'
0x61626364 = 'ABCD'		→ 0
CONVERT(0x61626364 USING latin1) = 'ABCD'	→ 1
```
```

Alternatively, for binary quoted strings or hexadecimal values, use an introducer to change the interpretation of the binary string:

```
```sql
_latin1 0x61626364 = 'ABCD'		→ 1
```
```

To cast a non-binary string to a binary string, use the `BINARY` keyword:

```
```sql
'abcd' = 'ABCD'			→ 1
BINARY 'abcd' = 'ABCD'		→ 0
'abcd' = BINARY 'ABCD'		→ 0
```
```

# ## 3.6 Choosing Data Types

Section 3.2, “MySQL Data Types,” described the various data types from which you can choose and the general properties of those types, such as the kind of values they may contain, how much storage space they take, and so on. But how do you actually decide which types to use when you create a table? This section discusses issues to consider that will help you choose.