Grep is short for "Get Regular ExPresssion," and in most versions of UNIX it comes in three slightly different versions. The first is the regular grep, which lets you search for text that matches some string of text that can include wildcards, character sets, and metacharacters. The second is fgrep (short for Fast grep, but it's actually slower), and the third is egrep (short for Extended grep), which extends the regular expression matching ability of grep and also lets you create logical OR expressions to search for. There are also some public-domain versions of grep that each have their own peculiarities and advocates, but we'll stick with the standard ones here. And for the most part, we'll stick with plain old grep, not the others.

# So how do I go about using grep?

In its basic form, the syntax of grep is:

```
grep [-options] regexpr [filename(s)]
```

where the options are

+   - **-b** Returns the block number as well as the matching line
+   - **-c** Returns only a count of the number of matching lines
+   - **-h** Returns only the matching lines, but not the filenames they were in
+   - **-i** Ignores case when matching
+   - **-l** Returns the filenames where there are matches, but not the matching lines
+   - **-n** Returns the line numbers in addition to the matching line
+   - **-s** Suppresses error messages
+   - **-v** Returns only lines that don't match the regular expression
+   - **-w** Matches only whole words (not available in all versions of grep)

Of these, the most useful are the -i option to ignore case and the -v option to reverse the search and return nonmatching lines.