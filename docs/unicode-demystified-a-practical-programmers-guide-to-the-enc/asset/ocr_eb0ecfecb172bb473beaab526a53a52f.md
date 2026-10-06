The first example that uses compound.in instructs sed to substitute the string words with text on lines 1, 2, and 3 and the string text with TEXT on lines 2, 3, and 4. The example also selects and deletes line 3. The result is text on line 1, TEXT on line 2, no line 3, and words on line 4. The sed made two substitutions on lines 2 and 3: for words and for text. Then sed deleted line 3:

```
$ cat compound
1,3 s/words/text/
2,4 s/text/TEXT/
3 d
```

```
$ sed -f compound.in
1. The text on this page...
2. The TEXT on this page...
4. The words on this page...
```

The next example shows that the ordering of instructions within a sed script is critical. Both Substitute instructions are applied to the second line, as in the pre-example, but the order in which the substitutions occurs change the result:

```
$ cat compound2
2,4 s/text/TEXT/
1,3 s/words/text/
3 d
```

```
$ sed -f compound2.in
1. The text on this page...
2. The text on this page...
4. The words on this page...
```

Next, compound3 appends two lines to line 2. The sed utility displays all the lines from the file once, because no -n option appears on the command line. The Print instruction at the end of the script displays line 3 an additional time:

```
$ cat compound3
2 a\nThis is line 2a.\nThis is line 2b.
3 p
```

```
$ sed -f compound3 compound.in
1. The words on this page...
2. The words on this page...
This is line 2a.
This is line 2b.
3. The words on this page...
3. The words on this page...
4. The words on this page...
```

The next example shows that sed always displays appended text. Here line 2 is deleted, but the Append instruction still displays the two lines that were appended to it. Appended lines are displayed if you use the -n option on the command line: