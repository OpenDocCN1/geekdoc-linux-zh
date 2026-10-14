```
## 50      60      472 states.txt
```

It makes sense that there are 50 lines, but it’s interesting that there are 60 total words. Let’s take a peak at the beginning of the file:

```
head states.txt
```

```
## Alabama
## Alaska
## Arizona
## Arkansas
## California
## Colorado
## Connecticut
## Delaware
## Florida
## Georgia
```

This file looks basically how you would expect it to look! You may recall from Chapter 3 that the kind of shell that we’re using is the bash shell. Bash treats different kinds of data differently, and we’ll dive deeper into data types in Chapter 5. For now all you need to know is that text data are called strings. A string could be a word, a sentence, a book, or a file or folder name. One of the most effective ways to search through strings is to use **regular expressions**. Regular expressions are strings that define patterns in other strings. You can use regular expressions to search for a sub-string contained within a larger string, or to replace one part of a string with another string.