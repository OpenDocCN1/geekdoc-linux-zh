
# Advanced Bash-Scripting Guide

As necessary, use the appropriate network analysis commands.

For some ideas, see Example 16-41 and Example A-28.

Optional: Write a script that searches through a list of e-mail messages and deletes the spam according to specified filters.

# Creating man pages

Write a script that automates the process of creating man pages.

Given a text file which contains information to be formatted into a man page, the script will read the file, invoke the appropriate grep commands to output the resulting man page to stdout. The text file contains blocks of information under the standard man page headings, i.e., NAME, SYNOPSIS, DESCRIPTION, etc.

Example A-39 is an instructive first step.

# Hex Dump

Do a hex(decimal) dump on a binary file specified as an argument to the script. The output should be in neat tabular fields, with the first field showing the address, each of the next 8 fields 4-byte hex, and the final field ASCII of the previous 8 fields.

The obvious followup to this is to extend the hex dump into a disassembler. Using a lookup table, or some other clever gimmick, convert the hex values into 0x86 op codes.

# Emulating a Shift Register

Using Example 27-15 as an inspiration, write a script that emulates a 64-bit shift register as an array. Implement functions to load the register, shift left, shift right, and rotate it. Finally, write a function that interprets the register contents as 8-bit ASCII characters.

# Calculating Determinants

Write a script that calculates determinants [153] by recursively expanding the minors. Use a 4 x 4 matrix as a test case.

# Hidden Words

Write a "word-find" puzzle generator, a script that hides 10 input words in a 10 x 10 array of letters. The words may be hidden across, down, or diagonally.

Optional: Write a script that solves word-find puzzles. To keep this from becoming too difficult, the solution will find only horizontal and vertical words. (Hint: Treat each row and column as a string, and search for substrings.)

# Anagramming

Anagram 4-letter input. For example, the anagrams of word are do or rod row. You may use /usr/share/dict/linux.words as the reference list.

# Word Ladders

A "word ladder" is a sequence of words, with each successive word in the sequence differing from the previous one by a letter.

For example, "mark --> ladder" from mark to vase:

```
mark ----> park ----> past ----> vast ----> vase
             ^         ^         ^         ^
```

Write a script that solves word ladder puzzles. Given a starting and an ending word, the script will list all intermediate steps in the "ladder." Note that all words in the sequence must be legitimate dictionary words.

# Fog Index

Appendix O. Exercises

The "fog index" of a passage of text estimates its reading difficulty, as a number corresponding roughly to a school grade level. For example, a passage with a fog index of 12 should be comprehensible to anyone with 12 years of schooling.

The Gunning version of the fog index uses the following algorithm.

1. Choose a section of the text at least 100 words in length.
2. Count the number of sentences (a portion of sentence truncated by the boundary of the section counts as one).
3. Find the average number of words per sentence.

```
AVE_WDS_SEN = TOTAL_WORDS / SENTENCES
```

4. Count the number of "difficult" words in the segment – those containing at least 3 syllables. Divide this quantity by total words to get the proportion of words.

```
PRO_DIFF_WORDS = LONG_WORDS / TOTAL_WORDS
```

5. The Gunning fog index is the sum of the two quantities, multiplied by 0.4, then rounded to the nearest integer.

```
G_FOG_INDEX = int (0.4 * (AVE_WDS_SEN + PRO_DIFF_WORDS))
```

Step 4 is by far the difficult portion of the exercise. There exist various algorithms for estimating syllable count of a word. A rule-of-thumb might consider the number of letters in a word and vowel-consonant mix. A strict interpretation of Gunning fog index does not count compound words and proper nouns as "difficult" words, but this would enumerate the script.

# Calculating PI using Buffon's Needle

The Eighteenth mathematician Buffon came up with a new experiment. Repeated a needle of length onto a wooden floor of long and parallel boards. The cracks separating the equal-width floor are a fixed distance d. Keep track of the total drops and the number of times the needle intersects a crack on the floor. The ratio of these two quantities turns out to a fractional multiple of PI.

In the spirit of Example 16-50, write a script that runs a Monte Carlo simulation of Buffon. To simplify, make the needle length equal to the distance between cracks, n = d. Hint: there are actually two variables: the distance from the center of the needle to the nearest crack, and the inclination angle of the needle to crack. You may use bc to handle the calculations.

# Playfair Cipher

Implement Playfair Cipher by substitution. It is traditional to use a 5x5 alphabetic key square for encryption and decryption.

```
C O D E S
A B G H I
K L M N P
Q R T U V
W X Y Z
```

Each letter of the alphabet appears once, except "I" also represents "J". The arbitrarily chosen word, "CODES" comes first, then all separate the plaintext message into digraphs (2-letter groups). If a group has two identical letters, delete the second, and form a new group. If there is a single letter left over the end, insert a "null" character, typically "X.".

For each digraph, there are three possibilities:

1) Both letters will be on the same row of the key square: each letter, substitute the one immediately to the right, in that row. If necessary, wrap around the beginning of the row.
2) Both letters will be in the same column of the key square: each letter, substitute the one immediately below it, in that row. If necessary, wrap around the top of the column.
3) Both letters will form corners of a rectangle within the key square: each letter, substitute the one on the other corner the rectangle which lies on the same row.

```
The "TH" falls under case #3.
G M
(Rectangle with "T" and "H" at corners)
T --> U
H --> G
```

The "SE" falls under case #1.
(Row containing "S" and "E")
S --> C (wraps around left of row)
E --> S
```

To decrypt text, reverse the above procedure under cases #1 and #2 (move in opposite direction for substitution). Under case #3, just take the remaining corners of the rectangle.

Helen Fouche' classic work, ELEMENTARY CRYPTANALYSIS (1939), gives fairly detailed description of the Playfair Cipher and its methods. This script will have three main sections:

I. Generating the key square, based on a user-input keyword.
II. Encrypting a plaintext message.
III. Decrypting encrypted text. The script will make extensive use of arrays and functions. You may use Example A-56 as inspiration. Please do not send the author solutions to these exercises. There are more appropriate ways to impress him with your cleverness, such as submitting bugfixes and suggestions for improving the book.

# Appendix P. Revision History

This document first appeared as a 60-page HOWTO in the late spring of 2000. Since then here the e-mail to the LDP requesting permission to submit version 0.1.

From <thegrendel@theriver> Sat Jun 10 09:05:33 2000 -0700
Date: Sat, 10 Jun 2000 09:05:28 -0700 (MSI)
From: "M. Leo Cooper"<thegrendel@theriver.com>
X-Sender: @localhost
To: ldp-discuss@linuxdoc.org
Subject: Permission to submit HOWTO

Dear HOWTO Coordinator,

I am working on and would like to submit to the LDP HOWTO on the subject of "Bash Scripting" (shell scripting, 'bash'). As it happens, I have been writing this document, off and on, for the last eight months or so, and I could produce a first draft in ASCII format in a matter of just a few more days.

I began writing out of frustration at being unable to find a decent book on shell scripting. I managed to locate some pretty good articles on various aspects of scripting, but nothing like a complete, beginning-to-end tutorial. Well, in keeping with my philosophy, if all fails, do it yourself.

As it stands, this proposed "Bash-Scripting HOWTO" would serve as a combination tutorial and reference, with the heavier emphasis on the tutorial. It assumes Linux experience, but only a very basic level of programming skills. Interspersed with the text are 79 illustrative examples of varying complexity, all liberally commented. There are examples for the reader.

At this stage, I'm up to 18,000+ words (124k), and that's over 50 pages of text (whew!).

I've mentioned that I've previously authored an LDP HOWTO "Software-Building HOWTO", which I wrote in Linuxdoc/SGML. I don't know if I could handle Docbook/SGML if I have you volunteers to do the conversion. People seem to have gotten on a more organized basis these last few months. Working with Greg Hanks and Tim Bynum was nice, but a professional team is even nicer.

Anyhow, please advise.

Mendel Cooper
thegrendel@theriver.com

# Table P-1. Revision History

| Release Date | Comments |
