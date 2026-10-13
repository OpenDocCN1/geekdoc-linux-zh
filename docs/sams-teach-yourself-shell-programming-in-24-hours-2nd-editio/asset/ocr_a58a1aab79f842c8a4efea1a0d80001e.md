+   - sort
+   - uniq

The tr command (short for transliterate) changes all the characters in one set into characters in a second set, whereas the sort command sorts the lines in an input file. The uniq command (short for unique) prints all the unique lines in a file.

The text of this chapter, ch15.doc, is used as the input file for the examples in this section.

# The tr Command

The first step in solving this problem is to eliminate all the punctuation and delimiters in the input file. You need to do this because the string 'end.' and the string 'end' are both the same word, end. You can accomplish this task using the tr command. The basic syntax for this command is

```
tr 'set1' 'set2'
```

Here all the characters in set1 are transliterated into the characters in set2. Usually, the characters themselves are used, but escape sequences covered in previous chapters can also be used.

To accomplish your first task, you can use the following command:

```
$ tr '!?";:[]{}(),.' ' ' < ch15.doc
```

Here you specified set2 as the space character because words separated by the characters in set1 need to remain separate after the punctuation is removed.

Notice that the characters [ and ] are given as \[ and \]. As you will see later in this chapter, these two characters have a special meaning in tr and need to be escaped using the backslash character (\ ) in order to be handled correctly.

> The tr command on some versions of Linux does not handle the \ escape sequence properly, used in the previous example, and might generate an error message similar to the following:
> 
> tr: invalid backslash escape '\['
> 
> You can work around this problem by using the punctuation class described later in this chapter.

At this point most of the words are separated by spaces, but some words might still be separated with tabs and newlines. To get an accurate count, all the words need to be separated by spaces, so you need to convert all tabs and newlines to spaces as follows:

```
$ tr '!?";:[]{}(),.\t\n' ' ' < ch15.doc
```