+   3. If the user types in bye, the computer replies with a message to say thanks for chatting and then finishes the program.

+   4. The program has stock responses for certain words, so it checks to see whether it recognizes any of the words the user has entered. If it does, it uses one of the appropriate stock responses. If more than one stock response applies, the computer chooses one at.

+   5. If none of the words is recognized, the program chooses a random phrase for its reply. To stop the random phrases from repeating, it replaces the phrase that's used with the word the user typed. Over time, the program learns from the user and starts to talk like her.

+   6. The program keeps chatting with the user until the user types in bye.

Now that you know the final goal, take your first steps toward it by setting up the random responses.

You can download the finished program from this book's website. See the Intro-duction for accessing the website.

![](bbox=[0.163, 0.378, 0.237, 0.442])

# Introducing lists

There are several different ways you can organize information in Python, and one of the most fundamental is called a list. We'll use lists to store the computer's random responses in the Chatbot program.

The following code shows how to create a list that has the name shopping_list. You can enter this code in the shell or create a program in the editor so that you can easily edit and refine it. To start a new program in the editor, use the File menu and select New. Your new file opens in a new tab in the editor. If you create a program, make sure you run it, so that the shopping list is set up.

If you enter the instructions in the shell, you can press Enter at the end of each line to go to a new line. Python will know you're not finished if you haven't given it final bracket.

```
shopping_list = [eggs",
  "bacon",
  "tomatoes",
  "bread",
  "tin of beans",
  "milk"]
```