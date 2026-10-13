As you can see in Figure 8.1, you are not able to see the file type if you don't have the proper permissions.

# cat

The concatenate (cat) command sends the text of a file to standard output. You can use the cat command on any file. The following command sends the text of the file to your screen:

```
cat file
```

# head and tail

The head and tail commands are like two sides of a coin. The head command provides you with a view of the first few lines of a file. The tail command provides you with a view of the last few lines of that same file. You can regulate the amount of the file that you see with switches. For example, if you were to use the following command, you'd see the first 15 lines of the bully.txt file.

```
head -n15 bully.txt
```

If you substitute tail for head, you'll see the last 15 lines of this file. Table 8.5 lists more switches for use with these commands.

# more and less

The more and less commands aren't opposites like head and tail. They both start at the beginning of a text file. When you run these commands on a text file, you review the contents of the file one page at a time. The less command is more versatile; unlike more, it allows you to scroll up and down any large text file with the Page Up and Page Down buttons on your keyboard.

Because they can read text a little bit at a time, these commands can open a file more quickly than a text editor like vi. The less command also has some of the advantages of the vi editor, because you can use some vi commands to search through a file.

**Table 8.5 head and tail commands.**

| Command | Result |
|---|---|
| head 400b bully.txt | You see the first 400 bytes of the file known as bully.txt. |
| tail 4k bully.txt | You see the final 4KB of the file known as bully.txt. |
| head 3m bully.txt | You see the first 3MB of the file known as bully.txt. |
| tail -n22 bully.txt | You see the final 22 lines of the file known as bully.txt. |