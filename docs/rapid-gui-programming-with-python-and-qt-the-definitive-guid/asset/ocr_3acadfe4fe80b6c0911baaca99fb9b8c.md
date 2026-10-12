# Table 1.3 Selected String Methods and Functions

| Syntax | Description |
| :--- | :--- |
| x in s | Returns True if string x is a substring of string s |
| x not in s | Returns True if x is not a substring of string s |
| x + s | Returns the concatenation of strings x and s |
| s * i | Returns a string consisting of int i concatenations of string s. For example, "Abc" * 3 produces "AbcAbcAbc" |
| len(s) | Returns the length of string s; this is a byte count if s is of type str and a character count if s is of type unicode |
| s.count(x) | Returns the number of times string x occurs in string s. This method, and several others, can take optional start and end arguments to restrict the search to a slice of the string they are called on. |
| s.endswith(x) | Returns True if string s ends with string x |
| s.startswith(x) | Returns True if string s starts with string x |
| s.find(x) | Returns the index position of the leftmost occurrence of x in s; returns -1 if x is not found |
| s.rfind(x) | Like find(), but searches from right to left |
| s.index(x) | Returns the index position of the leftmost occurrence of x in s; raises a ValueError exception if no x is found |
| s.rindex(x) | Like index(), but searches from right to left |
| s.isdigit() | Returns True if the string is not empty and the character or characters it contains are all digits |
| s.isalpha() | Like isdigit(), but checks for letters |
| s.join([x, ...]) | Returns a string which is the concatenation of the given sequence delimited by the string on which the method is called. For example, ":".join(["A", "BB", "CCC"]) returns "A:BB:CCC". The delimiter can be empty. |
| s.lower() | Returns a lower-cased copy of string s |
| s.upper() | Returns an upper-cased copy of string s |
| s.replace(x, y) | Returns a copy of string s with any occurrences of string x replaced by copies of string y |
| s.split() | Returns a list of strings, splitting on whitespace. For example, "ab\tc d e".split() returns ["ab", "c", "d", "e"]. This method can be given a first argument which is a string to split on, and a second argument which is the maximum number of splits to make. |
| s.strip() | Returns a copy of the string with leading and trailing whitespace removed. Accepts an optional string argument specifying which characters should be removed. |
| s.rstrip() | Returns a copy of the string with trailing whitespace removed. Accepts an optional string argument specifying which characters should be removed. |
| s.lstrip() | Returns a copy of the string with leading whitespace removed. Accepts an optional string argument specifying which characters should be removed. |