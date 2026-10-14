+   - Kincaid formula, originally developed for Navy training manuals; a good readability test for technical documentation
+   - Automated Readability Index (ARI)
+   - Coleman-Liau formula
+   - Flesch Reading Ease Score, which gives an approximation of readability from 0 (difficult) to 100 (easy)
+   - Fog Index, which gives a school-grade reading level
+   - wSTF Index, a readability indicator for German documents
+   - Wheeler-Smith Index, Lix formula, and SMOG-Grading tests, all readability indicators that give a school-grade reading level

# 11.3.4 Checking Text for Difficult Sentences

To output just the “difficult” sentences of a text, use style with the -r option followed by a number; style will output only those sentences whose Automated Readability Index (ARI) is greater than the number you give.

⇒ To output all sentences in the file dissertation whose ARI is greater than a value of 20, type:

```
$ style -r 20 dissertation [RET]
```

# 11.3.5 Checking Text for Long Sentences

Use style to output sentences longer than a certain length by giving the number of words as an argument to the -l option.

⇒ To output all sentences longer than 14 words in the file dissertation, type:

```
$ style -l 14 dissertation [RET]
```

# 11.4 Using Reference Files

There are reference works and other informative text files that you can install on your system; the following recipes describe some of the more interesting and useful ones that are readily available.

8 To get an idea how the ARI ranks text, see its rankings for various popular Web sites at http://www.readability.info/commonscores.shtml.