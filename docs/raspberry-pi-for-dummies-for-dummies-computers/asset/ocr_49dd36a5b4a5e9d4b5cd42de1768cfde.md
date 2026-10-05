This runs the dictionary_check() function and sends it the text "blue" to work with. When the function starts, Python puts "blue" into the function's variable called message and then prints onscreen the text that it contains. The text "hello" is sent by the function, but you don't have a way to pick up that message.

The next code snippet shows you how you can pick up information coming back from a function. Instead of just running the function, set a variable to be equal to its output, like this:

```
result = dictionary_check("red")nprint("Reply is:", result)
```

When the "hello" is sent back by the function, it goes into the variable result, and the main program can print it on the screen.

This simple example illustrates few reasons why functions are a brilliant idea and have fundamental building blocks in many programming languages:

+   **Functions enable you to reuse parts of your program.** For example, we used our function to display two different messages here, just by sending the function a different argument each time. When you use more sophisticated programs, being able to reuse parts of your program makes your work shorter, simpler, and faster to write.

+   **Functions understanding the program easier because they give a name and structure to a set of instructions.** Whenever someone sees dictionary_check() in our program, she can make a good guess at what's going on. So far, our programs haven't particularly complex, but on bigger projects, you'll find readability increasingly important.

+   **Functions make it easier to maintain and update your program.** You can easily find which bits of the program to change, and all the changes you need to make will in the same part of the program. If you think of a better way to do a dictionary-up lookup, you can just modify the function, without disturbing the rest of the program.

+   **Functions make testing and development easier.** We've built an experimental program that takes some text and sends back a message. What's the finished dictionary_check() will do, except that this one sends the same message back every time, and the one we built sends different messages based on what the user said. You could build the rest of the program around this simple test function to ensure that it works, and then go back and finish the dictionary_check() function.