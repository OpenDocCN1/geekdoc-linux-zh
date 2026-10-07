# 500 Lab : The read and printf Commands

g) What does the expression (( chars += $(#REPLY)) )) compute?

Answer: It adds the number of characters in each line to the variable chars.

Because there is no field splitting when the read command at the top of the loop is executed, REPLY contains all the characters in each line, including all spaces and tabs. (We'll deal with those new lines later.) We covered the use of $(# ... ) to find the number of characters in a string in Exercise 10.3.3, “Work with Strings and Substrings,”

h) Does the shell field splitting when the read command inside the loop is executed?

Answer: It uses the default value of IFS to field splitting “in the usual way.”

The idea here is by manipulating the value of IFS you can get the first read to input each line as an image of what is in the input file (except for the new lines) and then to get the second read to split the line into words, where a word is defined as a sequence of non-whitespace characters.

![](bbox=[0.135, 0.483, 0.223, 0.555])

When a read command does field splitting, it normally treats a backslash \) at the end of a line as a continuation marker and appends the “next” line of the file to the first one automatically.The -r option suppresses this behavior and is used in mywc so that whatever looks like a line in the file is counted as such.

i) What does the expression, (( words += $(#inWords[@]) )) compute?

Answer: It adds the number of elements in the array inWords to the integer variable words.

You can infer from this line and the output of the program that the second read command has split the input line into tokens and stored them as separate values in the array inWords. This is an extension of the idea of having multiple input buffers already discussed in the present exercise. By using ${#inWords[@]}, which was covered in Exercise 10.3.3, “Work with Strings and Substrings,” we get a count of how many elements there are in the array, which is the same as the number of tokens in the line.