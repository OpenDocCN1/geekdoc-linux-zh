want to translate your outline into Linux code. In any case, you want your outline to look something like the following example:

+   1. Start the bash shell.
+   2. Clear the screen.
+   3. Show the title.
+   4. Ask the user to enter his first name.
+   5. Wait for the user to enter the name.
+   6. Display a hello message using the user's name.
+   7. End the program.

Make note of the reserved words that you use in your outline. Avoid guessing. Feel free to look up the reserved words in this book. (I love an open book test, don't you?)

By the way, many programmers use an editor to create their outlines instead of paper and pencil. (An editor is a simple word processor, and I talk about editors in the section "Considering Your Options for Text Editors," later in this chapter.)

# Making your outline correspond to Linux code

Now you want to number each part of your Linux program to correspond to the line numbers on your program plan as you write your code. These numbers help you make sure that you don't skip a part of the program. But don't think that you need to know this code now. The following code section is just an example of how your code is going to look as you translate your outline into Linux code. Step 7 seems to be missing in this example. This step is the one that ends the program. You don't need to tell the computer when to end the program, however, because it knows to stop if it finds no more instructions.

```
1. #!/bin/bash
2. clear
3. echo "Welcome To My First Linux Program"
4. echo "Enter your first name: "
5. read response
6. echo "Hello, $response"
```

You want to remove the numbers from your program whenever you're ready to run the program. (Linux programs don't use line numbers.)