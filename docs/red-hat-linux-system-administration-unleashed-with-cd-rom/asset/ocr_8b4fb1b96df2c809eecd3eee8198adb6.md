everything else that appears on that line. Here is an example of a bash script with comments:

```
#!/bin/bash
# This is a bash script written to demonstrate comments
echo This program does nothing  # You can start a comment
# anywhere on a line
# this is the end of the program
```

When you run the preceding script, all it does is output the following line:

```
This program does nothing
```

All of the text that follows the pound symbol is ignored by bash, and as you can see, the pound symbols can start anywhere on a line. You should definitely get in the habit of using comments regularly in your bash scripts.

# Including Text Blocks

You can include blocks of text in your bash shell scripts by using the << operator followed by an identifier. The identifier signals the start of the text block and the end of the text block. This can be used to include a multiline comment in a shell script. Here is an example of a multiline comment:

```
#!/bin/bash
<< COMMENT
Bash ignores this:
COMMENT
```

You can also output blocks of text using the same method by including the cat command before you put the << symbol. For example, the following code outputs a welcome message:

```
#!/bin/bash
cat << MESSAGE
Welcome to my program
Thank you for running it!
MESSAGE
```

Running the preceding program will give you the following output:
Welcome to my program
Thank you for running it!
This method is useful when you have a lot of text to output because you do not have to put an echo command at the start of every line.