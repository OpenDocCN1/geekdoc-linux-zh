These functions are similar to LENGTH(), except that the argument length is counted in characters, not bytes. (Multi-byte characters are each counted as having a length of 1.)

+   CHARSET(str)

Returns the name of the character set of the given string, or NULL if the argument is NULL.

```
CHARSET('abc')               → 'latin1'
CHARSET(CONVERT('abc' USING utf8))          → 'utf8'
CHARSET(123)                   → 'binary'
```

+   COALESCE(expr1, expr2, . . . )

Returns the first non-NULL element in the list, or NULL if no argument is non-NULL.

```
COALESCE(NULL, 1/0, 2, 'a', 45+97)         → '2'
COALESCE(NULL, 1/0)                  → NULL
```

+   COERCIBILITY(str)

Returns the collation coercibility of a string, or NULL if the argument is illegal. Coercibility is the degree to which a string is subject to having its collation changed in expressions that involve other strings. The following table shows the return values, from lesser to greater coercibility.

| Coercibility | Meaning |
| :----------- | :----------- |
| 0 | Collation is explicit, cannot be coerced |
| 1 | No collation specified |
| 2 | Collation is implicit |
| 3 | Collation of system values such as USER() |
| 4 | Collation is coercible |
| 5 | Collation is ignorable (as for NULL) |

```
COERCIBILITY(_utf8 'abc' COLLATE utf8_bin)  → 0
COERCIBILITY('abc')                          → 4
```

+   COLLATION(str)

Returns the name of the collation of the given string, or NULL if the argument is illegal.

```
COLLATION(_latin2 'abc')              → 'latin2_general_ci'
COLLATION(CONVERT('abc' USING utf8) COLLATE utf8_bin)  → 'utf8_bin'
```