# ## Modifying strings

The Python `str` object has many useful methods that can be dot-suffixed to its name for modification of the string and to examine its contents. The most commonly used string modification methods are listed in the table below, together with a brief description:

| Method: | Description: |
| :-- | :-- |
| `capitalize()` | Change string’s first letter to uppercase |
| `title()` | Change all first letters to uppercase |
| `upper()` 
`lower()` 
`swapcase()` | Change the case of all letters to uppercase, to lowercase, or to the inverse of the current case respectively |
| `join( seq )` | Merge string into separator sequence `seq` |
| `lstrip()` 
`rstrip()` 
`strip()` | Remove leading whitespace, trailing whitespace, or both leading and trailing whitespace respectively |
| `replace( old , new )` | Replace all occurrences of `old` with `new` |
| `ljust( w , c )` 
`rjust( w , c )` | Pad string to right or left respectively to total column width `w` with character `c` |
| `center( w , c )` | Pad string each side to total column width `w` with character `c` (default is space) |
| `count( sub )` | Return the number of occurrences of `sub` |
| `find( sub )` | Return the index number of the first occurrence of `sub` or return -1 if not found |
| `startswith( sub )` 
`endswith( sub )` | Return True if `sub` is found at start or end respectively – otherwise return False |
| `isalpha()` 
`isnumeric()` 
`isalnum()` | Return True if all characters are letters only, are numbers only, or are letters or numbers only – otherwise return False |
| `islower()` 
`isupper()` 
`istitle()` | Return True if string characters are lowercase, uppercase, or all first letters are uppercase only – otherwise return False |
| `isspace()` | Return True if string contains only whitespace – otherwise return False |