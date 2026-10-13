# What Are Regular Expressions?

NEW TERM Regular expressions are patterns that use special syntax to match strings (usually in text in files, unless your search is for filenames). There are also extended regular expressions that can use additional operators in the search patterns. The difference, important for syntax, should not deter you from learning how to construct patterns that accurately match your desired search targets. This is important if you're looking for text in files and critical if you're performing potentially dangerous tasks, such as multiple file deletions across your system.

You can build an infinite number of regular expressions using only a small subset of pattern characters. Table 5.1 contains a short list of some of these characters. You should be familiar with at least one (the asterisk) from the previous examples.

**TABLE 5.1 COMMON REGULAR EXPRESSIONS**

| Expression | Matching |
|---|---|
| * | Any character |
| ? or . | A single character |
| {x} | Preceding character x times |
| {x,y} | Preceding character at least x times but no more than y |
| {x,} | Preceding character at least x times |
| (xxx)|(XXX) | String xxx or XXX |
| [xxx] or [x-x] | A character in a range of characters |
| [XYZ]+ | X, Y, or Z at least once |
| \x | A character such as ? or \ |
| ^pattern | pattern at the beginning of a line |
| $pattern | pattern at the end of a line |

This is not a comprehensive list of pattern characters. For more details, you can read the ed manual page (the ed command is discussed in Hour 14, “Text Processing”). For now, try several simple examples using different patterns.

The asterisk is useful for finding matches to all characters. For example, if you want to find all the text files in your directory with an extension of .txt, you can use the following:

```
# ls *.txt
14days.txt 96hours.txt datalog.txt datebook.txt day67.txt
```