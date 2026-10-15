```
chinese  ttys2  Dec  3 22:53  (excalibur)
cdemmert ttys5  Dec  3 23:00  (mentor)
```

Now type w six times more, noting that the cursor stops three times in the field to indicate what time the user logged in to the system (15:11 in this listing). Now your cursor should be sitting on the parenthesized field:

Click here to view code image

```
leungtc  ttys0  Nov 28 15:11  (gold)
chinese  ttys2  Dec  3 22:53  (excalibur)
cdemmert ttys5  Dec  3 23:00  (mentor)
```

# 5. It’s time to move backward. Type b a few times; your cursor moves backward, to the beginning of each word.

What happens if you try to move backward, and you’re already on the first word, or if you try to move forward with the w command, and you’re already on the last word of the line? Let’s find out.

# 6. Using the various motion keys you’ve learned, move back to the beginning of the line that starts with leungtc, which you used in instruction 4:

Click here to view code image

```
leungtc  ttys0  Nov 28 15:11  (gold)
chinese  ttys2  Dec  3 22:53  (excalibur)
cdemmert ttys5  Dec  3 23:00  (mentor)
```

This time, type W (uppercase W, not lowercase w) to move through this line. Can you see the difference? Notice what happens when you hit the time field and the parenthesized words. Instead of typing w seven times to move to the left parenthesis before gold, you can type W only five times.

# 7. Try moving backward using the B command. Notice that the B command differs from the b command the same way in which the W command differs from the w command.

Moving about by words, both forward and backward, being able to zip through half screens or full screens at a time, and being able to zero in on specific spots with the h, j, k, and l cursor-motion keys give you quite a range of motion. Practice using these commands in various combinations to get your cursor to specific characters in your sample file.

# Task 10.4: Inserting Text Using i, a, o, and O

Being able to move around in a file is useful. The real function of an editor, however, is to enable you to easily add and remove—in editor parlance, insert and delete—information. The vi editor has a special insert mode, which you must use to add to the contents of a file. Four possible ways exist to switch into insert mode from command mode, and you’ll learn about all of them in this task.

The first way to switch to insert mode is to type the letter i, which, mnemonically enough, inserts text into the file. The other commands that accomplish more or less the same thing are a, to append text to the file; o, to open a line below the current line; and O, to open a