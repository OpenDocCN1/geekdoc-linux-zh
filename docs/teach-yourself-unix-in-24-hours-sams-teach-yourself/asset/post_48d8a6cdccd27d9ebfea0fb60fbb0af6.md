
## Wildcards and Regular Expressions

If I want to see both bigfiles and the binary directory, I can use b* as a file pattern:

```
% ls -ld b*
-rw-rw-- 1 taylor 165 Dec 3 16:42 bigfiles
drwx------ 2 taylor 512 Oct 13 10:45 bin/
```

If I want to see all entries that start with a lowercase letter, I can explicitly type each one:

```
% ls -ld b* k* o* s* t*
-rw-rw-- 1 taylor 126 Dec 3 16:34 awkscript
-rw-rw-- 1 taylor 165 Dec 3 16:42 bigfiles
drwx------ 2 taylor 512 Oct 13 10:45 bin/
-rw-rw-- 1 taylor 12556 Nov 16 09:49 keyline.pie
-rw-rw-- 1 taylor 8729 Dec 2 21:19 owl.c
-rw-rw-- 1 taylor 199 Dec 3 16:11 sample
-rw-rw-- 1 taylor 207 Dec 3 16:11 sample2
drwx------ 2 taylor 512 Oct 13 10:45 src/
drwx------- 2 taylor 512 Nov 8 22:20 temp/
-rw-rw-- 1 taylor 582 Nov 27 18:29 tetme
```

That's clearly quite awkward. Instead, I can specify a range of characters. I specify the range by listing them all neatly inside a pair of square brackets:

```
% ls -ld [abkost]*
-rw-rw-- 1 taylor 126 Dec 3 16:34 awkscript
-rw-rw-- 1 taylor 165 Dec 3 16:42 bigfiles
drwx------ 2 taylor 512 Oct 13 10:45 bin/
-rw-rw-- 1 taylor 12556 Nov 16 09:49 keyline.pie
-rw-rw-- 1 taylor 8729 Dec 2 21:19 owl.c
-rw-rw-- 1 taylor 199 Dec 3 16:11 sample
-rw-rw-- 1 taylor 207 Dec 3 16:11 sample2
drwx------ 2 taylor 512 Oct 13 10:45 src/
drwx------- 2 taylor 512 Nov 8 22:20 temp/
-rw-rw-- 1 taylor 582 Nov 27 18:29 tetme
```

In this case, the files that start with an a, b, k, o, s, or t. This notation is still a bit clumsy and would be better if there were more files involved.

- 2. The ideal is to specify a range of characters using the hyphen character in the middle of a range:

```
% ls -ld [a-z]*
-rw-rw-- 1 taylor 126 Dec 3 16:34 awkscript
-rw-rw-- 1 taylor 165 Dec 3 16:42 bigfiles
drwx------ 2 taylor 512 Oct 13 10:45 bin/
-rw-rw-- 1 taylor 12556 Nov 16 09:49 keyline.pie
-rw-rw-- 1 taylor 8729 Dec 2 21:19 owl.c
-rw-rw-- 1 taylor 199 Dec 3 16:11 sample
-rw-rw-- 1 taylor 207 Dec 3 16:11 sample2
drwx------ 2 taylor 512 Oct 13 10:45 src/
drwx------- 2 taylor 512 Nov 8 22:20 temp/
-rw-rw-- 1 taylor 582 Nov 27 18:29 tetme
```

In this example, the shell will match any file that begins with a lowercase letter, ranging from a to z, as specified.

## Hour 9

3. Space is critical in all wildcard patterns, too. Watch what happens if I accidentally add a space between the closing bracket of the range specification and the asterisk following:

```
% ls -Cfd [a-z] *
Archives/ bigfiles owl.c src/
InfoWorld/ News/ bin/ sample temp/
Mail/ OWL/ keylime.pie sample2 femme
```

This time, the shell tried to match all files whose names were one character long and lowercase, and then it tried to match all files that matched the asterisk wildcard, which, of course, is regular files in the directory.

4. The combination of character ranges, single-character wildcards, and multi-character wildcards can be tremendously helpful. If I move to another directory, I can easily search for all files that contain a single digit, or underscore in the name:

```
% cd Mail
% ls -Cf
71075.446 emilyc mailbox sartin
72033.216 gordon_hat manley sent
bnciner harrism maralini
bob_gill travel marv
cennamo matt_ruby steve
dataylor john_welch mwcilla
taylordecc john
netflix.postings v8921
diserti ratcenter druby
dunlaplim lexb xdlf euts rustle
```
% ls *[0-9]_*
71075.446 euts matt.ruby xif
72033.216 gordon_hat news.postings
bob_gill john_welcher siob_n
dane_some v8921
```

I think the best way to learn about pervasive features such as wildcards is to use them. Flip through this book, I immediately notice that the examples are built earlier. This will continue the case, and the filename range shown here will be used again and again, in combination with the asterisk and question mark, to specify groups of files or directories. Remember that, if you want to experiment with wildcards, you can easily use the echo command because it dutiful prints the expanded version of any pattern you specify.

## Task 9.3: Creating Regular Expressions

A regular expression can be as simple as a word to match, such as acme, or as complex as the example in the script, "*[a-zA-Z]*", which matches all lines that begin with an upper or lowercase letter or contains z.

The language of regular expressions is full of punctuation characters and other letters used in unusual ways. It is important to remember that regular expressions are different from shell wildcards. It's unfortunate, but it's true. In shell, for example, a* lists any file that starts with the letter a. Regular expressions aren't left, which means you need to specify ^a if you want to match only lines that begin with the letter a. The pattern a* only filenames that start with the letter has a different interpretation completely when used as part of a regular expression.

| Notation | Meaning |
| :--- | :--- |
| c | Matches the character c |
| \c | Forces c to read as the letter c, not as another character might |
| ^ | Beginning of the line |
| $ | End of the line |
| [xy] | Any single character in the set |
| [^xy] | Any single character not in the set |
| c* | Zero or more occurrences of character c |

The notation isn't as complex as it looks in this table. The most important things to remember about regular expressions are that the * denotes zero or more occurrences of the previous character, and . is any single character. Remember that shell patterns use * to match any set of zero more characters independent of the previous character, and ? to match a single character.

## ACTION

1. The easy searches with grep are those that search for specific words without any special regular expression notation:

```
% grep /etc/passwd
taylorj?:1048:1375:James Taylor/users/taylorj/bin/csh
maylorj?:769:1375:Melanie Taylor/users/mtaylor/usr/local/bin/csh
daylorj?:375:1618:Dave Taylor/users/taylorj/usr/local/lib/msh
taylorrj?:203:1022:James Taylor/users/taylorrj/bin/csh
taylorrj?:662:1042:Robert Taylor/users/taylorrj/bin/csh
taylorm?:869:1508:Melanie Taylor/users/taylorm/bin/csh
taylorj?:1989:1412:Dave Taylor/users/taylorj/bin/csh
```

I searched for all entries in the passwd file that contain the pattern taylor.

2. I've found more matches than I wanted, though I don't want to see all alternatives. If I'm looking for my ^ character before the left-roots the pattern:

```
% grep "*taylor*" /etc/passwd
taylorj?:1048:1375:James Taylor/users/taylorj/bin/csh
taylorrj?:203:1022:James Taylor/users/taylorrj/bin/csh
taylorrj?:662:1042:Robert Taylor/users/taylorrj/bin/csh
taylorm?:869:1508:Melanie Taylor/users/taylorm/bin/csh
taylorj?:1989:1412:Dave Taylor/users/taylorj/bin/csxh
```

Now I want to narrow the search. I want to specify a pattern that says show me all lines that start with taylor, followed by a character that is not a lowercase letter.

3. To accomplish this, I use the [^xy] notation, which indicates an exclusion set of characters that cannot match:

```
% grep "^taylor[^a-z]" /etc/passwd
taylorj?:1048:1375:James Taylor/users/taylorj/bin/csh
taylorrj?:1989:1412:Dave Taylor/users/taylorj/bin/csh
```

It worked! You can specify two ways: You either list each character or use a hyphen to specify a starting character with the left of the hyphen and ending with the character to the right of the hyphen. That is, a-z is the range beginning with a and ending with z, and 0-9 includes all digits.

4. To see which accounts were excluded, remove the ^ for an inclusion range, which is a set of characters which one pattern must match:

```
% grep "^taylor[a-z]"" /etc/passwd
taylorj?:1048:1375:James Taylor/users/taylorj/bin/csh
taylorrj?:203:1022:James Taylor/users/taylorrj/bin/csh
taylorm?:869:1508:Melanie Taylor/users/taylorm/bin/csh
taylormx?:869:1508:Melanie Taylor/users/taylorm/bin/csh
```
