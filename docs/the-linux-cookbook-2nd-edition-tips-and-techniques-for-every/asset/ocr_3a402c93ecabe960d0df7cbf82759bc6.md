⇒ Here are two ways to use this.

+   - To output all anagrams of the word “lake,” type:
+     $ an lake RET
+   - To output all anagrams of the phrase “lakes and oceans,” type:
+     $ an 'lakes and oceans' RET

To limit the anagrams that are output to those containing a given string, specify that string with the -c option.

⇒ To output only anagrams of the phrase “lakes and oceans” that contain the string “seas,” type:
$ an -c seas 'lakes and oceans' RET

To print all of the words that can be made with some or all of the letters in a given word or phrase, use the -w option. This outputs words that are not anagrams, because anagrams must contain all of the letters of the other word or phrase.

⇒ To output all of the words that can be made from the letters of the word “seas,” type:
$ an -w seas RET

This command outputs all of the words that can be formed from all or some of the characters in “seas,” including “see” and “as.”

NOTES: There are other tools for finding anagrams, but this one is the best. Unfortunately, it isn’t widely available outside of the Debian distribution; if you can’t locate a copy, you can always install the sources from the Debian package (see Recipe 1.1.2 [Preparation of Recipes], page 3).

# 30.5.2 Finding Palindromes in Text

A palindrome is a word or phrase that reads the same both forwards and backwards; for example, “Mom,” “nun,” and “Madam, I’m Adam” are all palindromes.

Here are a few PERL “one-liners” for finding palindromes.

# METHOD #1

To output all lines in a file that are palindromes, use this simple PERL one-liner, and substitute the name of the file to check for file:

```
perl -ne 'map { print if $_ eq reverse } split' file
```