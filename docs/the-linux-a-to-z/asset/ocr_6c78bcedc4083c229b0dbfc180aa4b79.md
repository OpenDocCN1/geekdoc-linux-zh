```
$ sed -e s/:/_:/ -e /carey_/s//cew_/ pw.test
root_:awmku76tr43d6:0:0::/root/:/bin/sh
pc_:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
cew_:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
mot_:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
grex_:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
```

The idea here is to append an underscore to the end of each login name and, additionally, change the login name carey_ to cew_. These things are achieved with two editing actions, the first dealing with the underscore for all users, and the second dealing with the name change for carey. The only thing to notice here is that the substitution in the second editing action doesn't specify a regular expression. In cases like this, the last regular expression value encountered as part of a line address or previous substitute command will be used instead. This will be carey_ in this example, from the line address of the second editing action.

# 5.2.2 Character Translation

The tr command performs a character translation function similar to the y editing action of sed, with a few extras on top. It is a very quick and simple program to use, with typical applications like translating upper case letters to lower case or deleting punctuation. The tr program is a true filter in that it can only read text from the standard input and send the translated version to the standard output. The basic form of the tr command is:

```
tr str1 str2
```

where str1 and str2 are strings of characters. In general, the characters appearing in str1 will be translated into the corresponding characters in str2. An example of this is:

```
tr ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz
```

Obviously, this will translate all upper case letters to their lower case equivalents. A rather simpler way to achieve the same thing is to specify a contiguous range of characters by just the first and last characters in the sequence, separated by a hyphen (-), as in:

```
tr A-Z a-z
```

The implication of these examples is that the number of characters specified by the two string parameters needs to be the same. Obviously, there are two ways that this can be different. If str1 is shorter than str2 then the second string is truncated to the length of the first. If str2 is shorter than str1 then the second string is padded out to the length of first using the rightmost character of str2. So that: