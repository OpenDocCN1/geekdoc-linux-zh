# Wildcards and Regular Expressions

Here are some pronunciation tips. UNIX folk tend to refer to the “ as quote, the * single quote, and the * back quote. The * is star, the . is dot, the ^ is caret or circumflex, the $ is dollar, and the - is dash.

![](bbox=[0.125, 0.137, 0.237, 0.212])

What does this mean? It means that you can use see to list everyone reported by who doesn't have s as the first letter of his or her account. You can, perhaps a bit more interestingly, eliminate all blank lines from a file with see, too. I'll show you by returning to the test file:

```
% cat testme
Archives/OWL/ keytime.pie
InfoWorld/src/
Mail/bitnet.mailing-lists.Z temp/
News/drop.text.hqx
```

```
Archives/OWL/ keytime.pie
InfoWorld/src/
Mail/bitnet.mailing-lists.Z temp/
News/drop.text.hqx
```

```
Archives/OWL/ keytime.pie
InfoWorld/src/
Mail/bitnet.mailing-lists.Z temp/
News/drop.text.hqx
```

Now I'll use sed and clean up this output:

```
% sed "^/$/d" testme
Archives/OWL/ keytime.pie
InfoWorld/src/
Mail/bitnet.mailing-lists.Z temp/
News/drop.text.hqx
```

```
Archives/OWL/ keytime.pie
InfoWorld/src/
Mail/bitnet.mailing-lists.Z temp/
News/drop.text.hqx
```

7. These commands can be used in combination, course; to remove all blank lines, all lines that contain the word keyword, and substitute binHex for each occurrence of hqx, one sed can be used, albeit a complex:

```
% cat testme | sed "^/$/;keytime/$s/hqx/BinHex/g"
InfoWorld/src/
Mail/bitnet.mailing-lists.Z temp/
News/drop.text.hqx
```

```
Archives/OWL/ temp/
InfoWorld/src/
Mail/bitnet.mailing-lists.Z temp/
```