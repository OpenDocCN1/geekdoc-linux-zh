The hyphen denotes a range within the square bracket. To find any character, either uppercase or lowercase, you could use the following:

/[a-zA-Z]

To search for characters that normally have a special meaning, such as [, you can ignore, or escape, the special meaning by preceding the special character with a \ (backslash). To search for [ in vi, for instance, you would use the following sequence:

\[

This search finds the first occurrence of [.

# Beginning and End of Line Search

You can specify that you wish your pattern match to take place at only the beginning or end of a line. To specify a beginning of the line pattern match, use the ^ (caret) preceding your desired pattern, as shown in the following example:

/^Think

This matches Think only when it appears at the beginning of a line.

To specify an end-of-the-line pattern match, use a $ (dollar sign) following your desired pattern, as shown in the following example:

/last.$

This matches last. only when it is followed by a newline.