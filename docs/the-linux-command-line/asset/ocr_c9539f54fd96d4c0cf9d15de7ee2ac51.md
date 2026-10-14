to be searched for, followed by the Enter key. The cursor will move to the next location containing the search string. A search may be repeated using the previous search string with the n command. Here's an example:

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
```

Place the cursor on the first line of the file. Type:

```
/Line
```

followed by the Enter key. The cursor will move to line 2. Next, type n and the cursor will move to line 3. Repeating the n command will move the cursor down the file until it runs out of matches. While we have so far only used words and phrases for our search patterns, vi allows the use of regular expressions, a powerful method of expressing complex text patterns. We will cover regular expressions in some detail in a later chapter.

# Global Search And Replace

vi uses an ex command to perform search and replace operations (called “substitution” in vi) over a range of lines or the entire file. To change the word “Line” to “line” for the entire file, we would enter the following command:

```
:%s/Line/line/g
```

Let's break this command down into separate items and see what each one does:

| Item | Meaning |
|------|---------|
| : | The colon character starts an ex command. |
| % | Specifies the range of lines for the operation. % is a shortcut meaning from the first line to the last line. Alternately, the range could have been specified 1, 5 (since our file is five lines long), or 1, $ which means “from line 1 to the last line in the file.” If the range of lines is omitted, the operation is only |