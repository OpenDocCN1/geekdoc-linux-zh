
## SUMMARY

The C shell has the built-in capability for numeric integer data processing in terms of arithmetic, logic, and shift operations. Combined with the array processing feature of the language, this allows the programmer to write useful programs for processing large data sets with relative ease. The numeric variables can be declared and processed by using the @ and set commands.

The here document feature of the C shell allows standard input of a command in a script to be attached to data within the script. The use of this feature results in more efficient programs. The reason is that no extra file-related operations, such as file open and read, are needed, as the data is within the script file and has probably been loaded into the main memory when the script was loaded.

The C shell also allows the user to write programs that ignore signals such as terminal interrupt (<Ctrl+C>). This useful feature can be used, among other things, to disable program termination when it is in the middle of updating a file. The onintr command can be used to invoke this feature.

The C shell programs can be debugged by using the -x and -v options of the csh command, as in csh -xv filename. This technique allows viewing of the commands in the user's script after variable substitution but before execution.

## QUESTIONS AND PROBLEMS

- 1. Is the expr command needed in the C shell?
- 2. What is the here document? Why is it useful?
- 3. Modify the num_array_demo script in Section 15.3 so that it takes the numbers to be added as the command line arguments. Use the while control structure and integer arrays.
- 4. What is the difference between the following two commands if students is an array? See the second shell session in Section 15.3 for the current value of the students array. Explain your answer.
  - a. set UNIX_Authors = $students[1-2]
  - b. set UNIX_Authors = ( $students[1-2] )
- 5. The dext script in Section 15.4 takes a single name as a command line argument. Modify this script so that it takes a list of names as command line arguments. Use the foreach control structure to implement your solution.
- 6. The script in the canleave file discussed in Section 15.5 is designed to ignore keyboard interrupt. How can this program be terminated? Be precise.
- 7. Write a C shell script that takes integer numbers as command line arguments and displays their sum on the screen.

8. Write a C shell script that takes an integer number from the keyboard and displays the Fibonacci numbers equal to the number entered from the keyboard. Thus, if the user enters 7, your script displays the first seven Fibonacci numbers.

9. What are signals in UNIX? What types of signals can be intercepted in C shell scripts?

10. Enhance the code of Problem 7 so that it cannot be terminated by pressing <Ctrl+C>. When the user presses <Ctrl+C>, your script should give a message to the user and continue.

11. Modify the script in Problem 6 so that it reads integers to be added as a here document.

12. Enhance the onintr_demo script so that it takes the code word and the category of the code word (e.g., scientist, TV newscaster, politician, celebrity, movie, sportsperson) as input. It then informs the user of the category and gives 10 chances to the user to guess the code word.

13. Write a C shell script that implements the following menu options:

- a. Display the name of the central processing unit (CPU) used by your system.
- b. Display the name of the operating system used by your computer.
- c. Display the results of a. and b. on the screen separated by a vertical tab.
- d. Display the full pathnames for the commands that have been executed on your system.
- e. Display the maximum number of files a process may open.
- f. Display the maximum number of simultaneous processes a user may have on the system.

Your program should not terminate when the user presses <Ctrl+C>.

Hint: Review the manual pages for the following commands: hash, ulimit, uname.
