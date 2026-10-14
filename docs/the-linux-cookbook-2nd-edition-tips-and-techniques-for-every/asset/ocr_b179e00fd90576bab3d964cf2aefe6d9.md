an argument; with no argument, number reads a numeral from the standard input.

⇒ To output the English text equivalent of 100,000, type:
$ number 100000 [RET]

# 29.6 Using ROT13 Encryption

You may, from time to time, come across mention of ROT13. Or you may come across a message—especially on Usenet, or in old email archives—that ybxf yvxv gvff.

This is text encoded in ROT13 encryption, so named because each letter in the alphabet is rotated thirteen places over, so that (in a 26-letter alphabet) the first thirteen letters are substituted for the last thirteen, and vice versa. Therefore, in ROT13, "A" (the first letter of the alphabet) becomes "N" (the 13th letter of the alphabet), "B" becomes "O," "C" becomes "P," and so on all the way through:

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
becomes
N O P Q R S T U V W X Y Z A B C D E F G H I J K L M

This type of cipher, where letters are substituted by rotating the entire alphabet according to some offset, is known today as Julius Caesar's cipher, named after its most famous adopter.¹

There are two primary methods, both using filters, for encoding and decoding text in and out of ROT13. One, the traditional method, is to use tr to transpose the characters, giving a set of the first and last 13 letters to transpose from, and a set of the last and first 13 letters to transpose to.

The second method automates this process with a tool called rot13, part of the bsd-games package. This package also includes caesar, a tool for decoding Caesar ciphers in general via statistical analysis of input.

ROT13 is not intended as a method for general encryption—it's much too easy to figure out—but it's good for when you want to temporarily obscure some text, such as the punch line of a joke or the "spoiler" portion of a movie review. To encode some text, make it a selection in X and then send it through one of the two filters for encoding it, or just type it as input to either filter. To decode some lines of ROT13 in text, do the same thing: make a selection of the encoded text, and then pass it through either of the filters (see Recipe 10.3 [Manipulating Selections of Text], page 253); press CTRL-D to terminate and exit the filter.

> ¹ According to Suetonius, Caesar's cipher had an offset of 4.