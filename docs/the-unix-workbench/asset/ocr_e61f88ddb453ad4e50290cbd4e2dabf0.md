+   ## New Hampshire
+   ## New Jersey
+   ## New Mexico
+   ## New York

In the previous case the regular expression we used was simply "New", which represents an occurrence of the string "New". Regular expressions are not limited to just being individual characters or words, they can also represent parts of words. For example I could search all of the state names that contain the string "nia" with the following command:

```
grep "nia" states.txt
```

+   ## California
+   ## Pennsylvania
+   ## Virginia
+   ## West Virginia

All of the state names above happen to end with the string "nia".

# Metacharacters

Regular expressions aren't just limited to searching with characters and strings, the real power of regular expressions come from using metacharacters. Remember that metacharacters are characters that can be used to represent other characters. To take full advantage of all of the metacharacters we should use grep's cousin egrep, which just extends grep's