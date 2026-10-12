arrays `s` . The arguments 5 and 6 are passed to the function to indicate the number of characters in `s` and `s` , respectively.

After the c function has completed execution and returns to m , a f loop is set up to display the results of the function call. The 11 elements of `s` are displayed, and as you can see from the program's output, the c function seems to be working properly. In the preceding program example, it is assumed that the first argument to the c function—the result array—contains enough space to hold the resulting concatenated character arrays. Failure to do so can produce unpredictable results when the program is run.

# Variable-Length Character Strings

You can adopt a similar approach to that used by the c function for defining other functions to deal with character arrays. That is, you can develop a set of routines, each of which has as its arguments one or more character arrays plus the number of characters contained in each such array. Unfortunately, after working with these functions for a while, you will find that it gets a bit tedious trying to keep track of the number of characters contained in each character array that you are using in your program—especially if you are using your arrays to store character strings of varying sizes. What you need is a method for dealing with character arrays without having to worry about precisely how many characters you have stored in them.

There is such a method, and it is based upon the idea of placing a special character at the end of every character string. In this manner, the function can then determine for itself when it has reached the end of a character string after it encounters this special character. By developing all of your functions to deal with character strings in this fashion, you can eliminate the need to specify the number of characters that are contained inside a character string.

In the C language, the special character that is used to signal the end of a string is known as the *null* character and is written as ' . So, the statement

```
Click here to view code image
 
c
```

defines a character array called w that contains *seven* characters, the last of which is the null character. (Recall that the backslash character [ is a special character in the C language and does not count as a separate character; therefore, ' represents a single character in C.) The array w is depicted in *Figure 9.2*.