# ## 7. Working with Functions

Behind all well-written programs in the C programming language lies the same fundamental element—the function. You’ve used functions in every program that you’ve encountered so far. The p and s routines are examples of functions. Indeed, each and every program also uses a function called m . You may be wondering, “What’s the big deal about functions?” When you start breaking down the your programming task into functions, your code will be easier to write, read, understand, debug, modify, and maintain. Obviously, anything that can accomplish all of these things is worthy of a bit of fanfare. As a result this is a chapter packed with important information, including

+   1. Understanding the basics of functions.
+   2. Explaining local, global, automatic, and static variables.
+   3. Using single-dimensional and multi-dimensional arrays with functions.
+   4. Returning data from functions
+   5. Using functions to execute top-down programming
+   6. Calling functions from within other functions, as well as recursive functions.

# ### Defining a Function

First, you must understand what a function is, and then you can proceed to find out how it can be most effectively used in the development of programs. Go back to the very first program that you wrote (Program 2.1), which displayed the phrase “Programming is fun.”:

Click here to view code_image

```
#
i
{

t
n
f
}
```

Here is a function called p that does the same thing:

Click here to view code_image

```
v
{
f
}
```

The differences between p and the function m from Program 2.1 is in the first and last line. The first line of a function definition tells the compiler (in order from left to right) four things about the function:

+   1. Who can call it (discussed in Chapter 14, “Working with Larger Programs”)
+   2. The type of value it returns
+   3. Its name
+   4. The arguments it takes

The first line of the p function definition tells the compiler that the function