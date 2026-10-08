+   8. Writing code to test and determine if user input is correct is known as \_\_\_\_\_\_\_\_\_\_.
a. algorithm design
b. data validation
c. flowcharting
d. pseuodocode design

9. If `.numeric_functions` is a script file of shell functions, the \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ command is used to load it into memory.
a. numeric_functions
b. load numeric_functions
c. .numeric_functions
d. install numeric_functions

10. True or false: shell functions may be executed from the command line.

# EXERCISES

+   1. From the command line create the function dir to execute this: `ls -l | more`.

2. From the command line create the function simple_date to execute this: `date +%D`.

3. Create the executable script file `.mystuff` to contain the two functions created in Exercises 1 and 2, and to call each function from the command line.

4. In the Lesson A exercises, you created the file my_old_cars. Write a shell script that allows the user to enter a search string and displays all records in the file that contain a string matching the search string. For example, if the user enters "Ford", the script displays all records that contain the word "Ford."

5. Write a shell script that allows the user to enter a search string and deletes all records in the my_old_cars file that contain a string matching the search string. For example, if the user enters "1948," the script deletes all records containing "1948."

6. Create shell functions that sort the records in the file my_old_cars. Your functions should sort the records by year model (the first field), by make (the second field), and by car model (the third field). Write a menu program that calls each sort function.

7. Write a Main menu program for the my_old_cars file and all the script files you have created so far. Here is a list of the script files you should have:

+   - Data entry screen
- Script that displays all records in the file
- Script that searches for and displays records containing a string
- Script that deletes specified records from the file
- Script that displays the records sorted in various ways