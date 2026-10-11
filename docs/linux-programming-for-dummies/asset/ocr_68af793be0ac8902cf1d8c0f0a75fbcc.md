# ## Chapter 13

# # Waxing Efficient with Functions (So You Don’t Have to Retype Code!)

**In This Chapter**

+   ▪ Creating a function
+   ▪ Calling a function
+   ▪ Passing arguments to a function
+   ▪ Sharing a function with a subprogram
+   ▪ Returning a value from a function

As you begin to write Linux programs, you find yourself repeating the same commands over and over again. You may want to personalize and print an invitation to your next bash (pardon the pun), for example, and then send the invitation to your friends. You can write the message inside a `for` in loop and place your friends’ names in a *wordlist*, which you can read about in Chapter 11. You can also rewrite the invitation many times in your program for each of your friends. Or you can use a function.

A *function* is part of your Linux program that you set aside from the rest of the program. Think of a function as a compartment inside your program. You identify a function with a unique name (known as, logically enough, a *function name*), and then you store one or more commands that you frequently use inside the function.

You can enter the name of the function in your program whenever you want Linux to use the commands that you store in the function. You can, thereby, use the same commands over and over simply by using the name of the function instead of rewriting all those commands again. I’d place the invitation to my bash inside a function.