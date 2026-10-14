# PIPES: PUMP A PROGRAM'S OUTPUT INTO ANOTHER PROGRAM

Linux provides you with a wide array of utilities to manipulate data. You can search, sort, slice, dice, and transform data stored in files in many different ways. A pipe (also called a pipeline) is a powerful shell feature that allows you to pump the output of one program directly into another.

For example, say you have a file with information about a group of people, including a name, age, zip code, and phone number for each person, that looks like this:

Roosevelt Tommy 38 54579 555-1212
Nixon Edward 19 37583 246-3457
Roosevelt Freddie 47 11745 674-6972
Lincoln Albert 26 26452 916-5763

If you wanted to find all the Roosevelts and sort them by zip code, you could do it like this:

```
grep Roosevelt people.txt > grep.out
sort +3 grep.out
rm grep.out
```

Since I haven't introduced the grep and sort commands yet, here's an English translation of what's happening above:
Look for lines that contain Roosevelt in the people.txt file and put them in a file named grep.out. Then sort the grep.out file on the fourth column and display the results on the console before deleting the grep.out file. (Yes, it is odd that the +3 flag tells sort to use the fourth column!)
But you could avoid creating and deleting the intermediate file (grep.out) by combining the operation into one command like this:

```
grep Roosevelt people.txt | sort +3
```

The vertical bar tells the shell that the output of the program on the left (grep) should become the input for the program on the right (sort). Behind the scenes, the shell may be issuing the exact same three commands as in the previous example, but you don't really care—you've combined three commands into one.