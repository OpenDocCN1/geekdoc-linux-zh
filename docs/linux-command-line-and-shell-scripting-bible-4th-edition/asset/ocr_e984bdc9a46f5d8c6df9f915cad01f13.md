| [ , d ] ) | index values are replaced with sequential numbers indicating the new sort order. Alternatively, the new sorted array is stored in array d if specified. |
|---|---|
| asorti( s [ , d ] ) | Sort an array s based on the index values. The resulting array contains the index values as the data element values, with sequential number indexes indicating the sort order. Alternatively, the new sorted array is stored in array d if specified. |
| gensub( r , s , h [ , t ] ) | Search either the variable $0 , or the target string t if supplied, for matches of the regular expression r . If h is a string beginning with either g or G, replaces the matching text with s . If h is a number, it represents which occurrence of r to replace. |
| gsub( r , s [ , t ] ) | Search either the variable $0 , or the target string t if supplied, for matches of the regular expression r . If found, substitute the string s globally. |
| index( s , t ) | Returns the index of the string t in string s, or 0 if not found. |
| length([ s ] ) | Returns the length of string s , or if not specified, the length of $0 . |
| match( s , r [ , a ] ) | Returns the index of the string s where the regular expression r occurs. If array a is specified, it contains the portion of s that matches the regular expression. |
| split( s , a [ , r ] ) | Splits s into array a using either the FS (field separator) character, or the regular expression r if supplied. Returns the number of fields. |
| sprintf( format , variables ) | Returns a string similar to the output of printf using the format and variables supplied. |
| sub( r , s [ , t ] ) | Search either the variable $0 , or the target string t , for matches of the regular expression r . If found, substitutes the string s for the first occurrence. |
| substr( s | Returns the nth character substring of s , starting at index |