# EXAMPLE 6.171 (CONTINUED)

We expect that everything will be completed and ready for shipment as scheduled on 5/18/2004.

Sincerely,

Dana Smith, Mgr

# EXPLANATION

+   1. In the BEGIN block, the field separator (FS) is assigned a colon, and a user-defined variable n is assigned 1.

+   2. In the while loop, the getline function reads a line at a time from the file called form.letter. If getline fails to find the file, it returns a -1. When it reaches the end of file, it returns 0. Therefore, by testing for a return value of greater than 1, we know that the function has read in a line from the input file.

+   3. Each line from form.letter is assigned to an array called form.

+   4. The output from the UNIX/Linux date command is piped to the getline function and assigned to the user-defined variable d. The split function then splits up the variable d with whitespace, creating an array called today.

+   5. The user-defined variable thisday is assigned the month, day, and year.

+   6. The BEGIN block ends.

+   7. The for loop will loop n times.

+   8. The user-defined variable temp is assigned a line from the form array.

+   9. The nested for loop is looping through a line from the input file, data.form, NF number of times. Each line stored in the temp variable is checked for the string @date. If @date is matched, the gsub function replaces it with today's date (the value stored in thisday).

+   10. If a # and a number are found in the line stored in temp, the gsub function will replace the # and number with the value of the corresponding field in the input file, data.form. For example, if the first line stored is being tested, #1 would be replaced with Dynamo, #2 with John Stevens, #3 with Dana Smith, #4 with 4/12/2004, and so forth.

+   11. The line stored in temp is printed after the substitutions.

# 6.25.4 Interaction with the Shell

Now that you have seen how awk works, you will find that awk is a very powerful utility when writing shell scripts. You can embed one-line awk commands or awk scripts within your shell scripts. The following is a sample of a Korn shell program embedded with awk commands.