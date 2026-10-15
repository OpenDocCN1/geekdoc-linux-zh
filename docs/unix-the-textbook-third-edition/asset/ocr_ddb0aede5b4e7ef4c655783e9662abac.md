# TABLE 16.6 (CONTINUED) Python Syntax and Command Summary

| Common List Methods | Result/Returns |
|---|---|
| L.method() | |
| append(obj) | Append obj to end of L |
| count(obj) | Returns int nbr of occurrences of obj in L |
| index(obj) | Returns index of first occurrence of obj in L; raises ValueError if obj not in L |
| pop([index]) | Returns item at specified index or item at end of L if index not given; raises IndexError if L is empty or index is out of range |
| remove(obj) | Removes first occurrence of obj from L; raises ValueError if obj is not in L |
| reverse() | Reverses L in place |
| sort() | Sorts L in place |
| Common Tuple Methods | Returns |
| T.method() | |
| count(obj) | Returns nbr of occurrences of obj in T |
| index(obj) | Returns index of first occurrence of obj in T; raises ValueError if obj is not in T |
| Common Dictionary Methods | |
| D.method() | Result/Returns |
| clear() | Remove all items from D |
| get(k, [val]) | Return D[k] if k in D, else val |
| has_key(k) | Return True if k in D, else False |
| items() | Return list of key-value pairs in D; each list item is two-item tuple |
| keys() | Return list of D's keys |
| pop(k, [val]) | Remove key k, return mapped value or val if k not in D |
| values() | Return list of D's values |
| Common File Methods | Result/Returns |
| F.method() | |
| read([n]) | Return str of next n chars from F, or up to EOF if n not given |
| readline([n]) | Return str up to next newline, or at most n chars if specified |
| readlines() | Return list of all lines in F, where each item is a line |
| write(s) | Write str s to F |
| writelines(L) | Write all str in seq L to F |
| close() | Closes the file |