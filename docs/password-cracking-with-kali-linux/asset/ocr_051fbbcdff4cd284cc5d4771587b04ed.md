# ## HYBRID ATTACKS – WORDLISTS AND BRUTE FORCE TOGETHER

Using a wordlist together with a mask is a much more efficient use of time.

The format for a hybrid attack is:

```
*-a6 wordlist [mask] or -a7 [mask] wordlist*
```

+   1. Using a -a6 attack:

```
*-a6 wordlist.txt ?a?!?l?u?s* (only the end of the hashcat command line is shown)
```

Will produce words like:

+   * catRaiN!  
+     cat7laB$  
+     dog\*upW)

+   2. Using an -a7 attack:

```
*-a7 ?a?!?l?u?s wordlist.txt*
```

Would produce words like:

+   * RaiN!cat  
+     7laB$cat  
+     \*upW)dog

You can add in the "-I" or incremental flag on any of the brute force methods, this causes Hashcat to only process one character of the mask at a time. So it will go through the entire wordlist and add just the "?a" character to each word. The second pass it will add the "?a?l", and so forth until all the characters in the mask are used.

First pass:

catB