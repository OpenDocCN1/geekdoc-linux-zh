
# ASSEMBLY LANGUAGE STEP-BY-STEP

original number C in the 16s column. Write a C down to the right of your 1:1C. So far, so good.

We've got the 16s column, so just as the 256s, we have to remove the 16s from what's left of the original number. The total value of the 16s column is C x 16 = 12 x 16 = 192. Bring the 193 value out of your calculator's memory, and subtract 192 from it. A lonely little 1 is all that's left.

So we're down to the units column. There is one unit in one, obviously. Write that 1 down to the right of the C in our hexadecimal number: 1C. Decimal 449 is equivalent to hex 1C.

Now perhaps you'll begin to understand why programmers use hexadecimal calculators so much.

Let's glance back at the big picture of the decimal-to-hex conversion. We're looking for the hexadecimal columns hidden in the decimal value. We find the largest column contained in the decimal number, find column's value, and subtract that value from the decimal number. Then we look for the next smallest hex column, and the next smallest, and so on, removing the value of each column from the decimal number as we go. In a sense, we're dividing the number by powers of 16 and keeping a running remainder by removing each column as we tally it.

Let's try it again. The secret number is 988,664.

1. Find the largest column contained in 988,664 from Table 2.6: 65,536. 988,664 / 65,536 = 15 and change. Ignore the change. 15 = F in hex. Write down the F.
2. Remove F x 65,536 from 988,664. Store the remainder: 5,624
3. Move to the next smallest column. 5,624 / 4,096 = 1 and change. Write the one.
4. Remove 1 x 4,096 from the remainder: 5,624 - 4096 = 1528. Store the new remainder: 1,528.
5. Move to the next smallest column. 1,528 / 256 = 5 and change. Write the five.
6. Remove 5 x 256 from the stored remainder, 1,528. Store 248 as the new remainder.
7. Move to the next smallest column. 248 / 16 = 15 and change. 15 = F in hex. Write down the F.
8. Remove F x 16 from stored remainder, 248. The remainder, 8, is the number of units in the final column. Write down the 8.

There you have it: 888,664 decimal = F15F8H.

Note the presence of the H at the end of the hex number. From now on, every hex number in the text of this book will have H affixed to its hindparts. It’s important, because not every hex number contains letter digits. There is a 157H as surely as a 157 decimal, and the two are not the same number. (Quick, now: By how many are they different?) Don’t get that H in writing your assembler programs, as I’ll be reminding you later on.

# Practice. Practice! PRACTICE!

The best (actually, the only) way to get a gut feel for hex notation is to use lots. Convert each of the following hex numbers to decimal. Lay each number out on the dissection table and identify how many 1s, how many 16s, how many 256s, how many 4,096s, and so on, are present in the number, and add them up to decimal.

- CCH
- 157H
- D8H
- BB29H
- 7AH
- 8177H
- A011H
- 99H
- 2B36H
- FACEH
- 8DB3H
- 9H

That done, now turn it inside out, and convert each of the following decimal numbers to hex. Remember the general method: From Table 2.6, choose the largest power of 16 that is less the decimal number to be converted. Find out how many times that power of 16 is present in the decimal number, and write it down as the leftmost hex digit of the converted number. Then subtract the total value represented by that hex digit from the decimal number. Then repeat the process, using the next smallest power of 16 until you’ve subtracted the down to nothing.

- 39
- 413
- 22
- 67,349
- 6,992
- 41
- 1,117
- 44,919
- 12,331
- 124,217
- 91,198
- 307
- 112,374,777

(Extra credit for that one ...) If you need more practice, choose some decimal numbers and convert them to hex, and then convert them back.

# Arithmetic in Hex

As you become more and more skilled in assembly language, you'll be doing more and more arithmetic in base 16. You may even (good grief) come to do it in your head. Still, it takes some practice.

Addition and subtraction are nothing more than what we know in decimal, with a few extra digits tossed in for flavor. The trick is nothing more than knowing your addition tables to 0FH. This is best done by thinking to yourself, “Now, if C is 12 and F is 15, then C + F is 12 + 15, which is 27 decimal but 1BH.” Instead, you should simply say inside your head, “C + F is 1BH.”

Yes, that's asking a lot. But I ask you now, as I will ask you again on this journey, do you wanna hack assembly ... or do you just wanna feel around? It takes practice to learn the piano, and it takes practice to get really greased up on the foundation concepts of assembly language programming.

So let me remind old school and tell you to memorize the following. Make flash cards if you must:

| 9 | 8 | 7 | 6 | 5 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 0AH | 0AH | 0AH | 0AH | 0AH |
| A | 9 | 8 | 7 | 6 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 0BH | 0BH | 0BH | 0BH | 0BH |
| B | 9 | 8 | 7 | 6 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 0CH | 0CH | 0CH | 0CH | 0CH |
| C | B | A | 9 | 8 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| ODH | ODH | ODH | ODH | ODH |
| D | C | B | 9 | 8 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| OEH | OEH | OEH | OEH | OEH |
| E | D | C | B | A |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| OFH | OFH | OFH | OFH | OFH |
| F | E | D | C | B |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 10H | 10H | 10H | 10H | 10H |
| F | E | D | C | B |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 11H | 11H | 11H | 11H | 11H |
| A | D | A | B | A |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 12H | 12H | 12H | 12H | 12H |
| C | B | A | 9 | 8 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 13H | 13H | 13H | 13H | 13H |
| B | A | 9 | 8 | 7 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 14H | 14H | 14H | 14H | 14H |
| A | C | B | A | 9 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 15H | 15H | 15H | 15H | 15H |
| D | C | B | A | E |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 16H | 16H | 16H | 16H | 16H |
| B | A | 9 | 8 | 7 |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 17H | 17H | 17H | 17H | 17H |
| A | C | B | A | F |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 18H | 18H | 18H | 18H | 18H |
| E | D | C | B | A |
|---|---|---|---|---|
| +1 | +2 | +3 | +4 | +5 |
| 19H | 19H | 19H | 19H | 19H |

```
F E D
+A +B +C
19H 19H 19H

F E D
+B +C +D
1AH 1AH 1AH

F E
+C +D
1BH 1BH

F E
+D +E
1CH 1CH

F
+E
1DH

F
+F
1EH
```

If nothing else, this exercise should make you glad computers don’t work in base 64.

# Columns and Carries

With all the single-column additions (more or less) to memory, you can tackle multicolumn addition. It works pretty much the same way it does with decimal. Add each column starting from the right, and carry into the next column anytime a single column’s sum exceeds 0FH.

For example:

```
1 1
2 F 3 1 A DH
+ 9 6 B A 0 7H
C 5 E B B 4H
```

Carefully work this one through, column by column. The sum of the column (that is, the rightmost) is 14H, which cannot fit in a single column, so we must carry the one into the next column to the left. Even

# Alien Bases

with the additional 1, however, the sum of the second column is 0BH, which fits in a single column and no carry is required.

Keep on adding toward the left. The second-to-last column will again overflow, and you will need to carry the one into the last column. as long as you have your single-digit sums memorized, it's a snap.

Well, more or less.

Now, here's something you should take note of:

The most you can ever carry out of a single-column addition of two numbers is 1.

It doesn't matter what base: 16, 10, fooby, or 2. You will either carry a 1 (in Martian, foo) out of a column, or carry nothing at all. This fact surprises people for some reason, so ask yourself: What two digits in old familiar base 10 can you add that will force you to carry a 2? The largest digit is 9, and 9+9 = 18. Put down the 8 and carry the 1. Even if you have to add a carry from a previous column, that will bring you (at most) to 19. Again, you carry a 1 and no more. This is important when you add numbers on paper, or within the silicon of your CPU, as you will learn a few chapters on.

# Subtraction and Borrows

If you have your single-column sums memorized, you can usually grind your way through subtraction with a shift into a sort of mental reverse: “If E+6 equals 14H, then 14H-E must equal 6.” The alternative is memorizing an even larger number of tables, and since I haven't memorized them, I won't ask you to.

But over time, that's what tends to happen. In subtraction, you should be able to dope out any given single-column subtraction by turning a familiar hexadecimal inside-out. And with base 10, multicolumn subtractions are done column by column, one column at a time:

```
F76CH
-A05BH
571H
```

During your inspection of each column, you should be asking yourself: “What number added to the bottom number yields the top number?” Here, you should know from your tables that B+1 = C, so the difference