control things such as the font and size of the letters are missing from the file. Try to find a readme or readme.txt file on your hard disk. These files sometimes come with other software to keep you up-to-date on the latest changes occurring with the program.

If you can't find any text files, however, you can use vi to create one. Just begin vi; press i to enter the input mode, and then type a whole bunch of lines on the page. Hey, why not just type some of the Linux code that you see in this book? You may go on to the next page if you go overboard with your typing — but that's just fine.

# Just line up

The vi text editor displays your text on lines shown on-screen. It automatically places the cursor on the first character of the first line of the text. Each line of text (including those lines that can't fit on-screen but exist in the file) has a number. The first line is number 1; the second line is number 2, and so on.

You can display the number of the line that the cursor is on by pressing Ctrl-G, I do that in Figure B-2, where I have my first program open. Notice that the line number appears at the bottom of the screen. (The cursor is on line 3 of a 14-line file.)

![](bbox=[0.08, 0.59, 0.85, 0.92])

```
Set flag = "go"
while ($flag = "go")
"Cho "Enter your name or type stop to end: "
"set friend = $
if ($friend = "stop") then
set flag = "stop"
break
endif
if ($friend = "tom") then
continue
endif
echo "Hello, $friend!"
end
echo "Good-bye!"
```