+   d. Converts all of the list elements to integer numbers, and

+   e. Produces a new integer list of the squares of all the integers, and finally

+   f. Prints the list of the squares of all the integers.

Then, test the function for your error handling statements with erroneous file names, or names of files that are not in the current working directory.

# 13. Modify the code in arith1.py from Example 16.19 so that the variable c is declared as a global variable in all four functions (add, subtract, multiply, and divide). For example:

```
def add(a,b):
    global c
    c = a + b
#NO RETURN STATEMENT!
```

Then:

+   a. Save the file as arith2.py.

+   b. Import arith2, and redo in-chapter Exercise 16.10.

+   c. Explain the results you get when you type >>>arith2.c on the Python command line at any particular point after you have imported and invoked the file arith2 with some numeric arguments.

# 14. Take the Bourne shell script named cmdargs_demo, shown in Section 12.4, and convert it to Python code that runs using Way 2 (Script mode). Your Python conversion should find the byte sizes of all ordinary (regular) and dot (.) files in the directory specified as an argument to the command, and add them up to print a total. It should skip over subdirectories. It should include the branching structure for error handling statements from the original Bourne shell script.

Hint: The following line of Python code adds up or accumulates the running total of file byte sizes of ordinary and dot files in the directory specified:

```
x = sum(os.path.getsize(f) for f in os.listdir(directory) if os.path.isfile(f))
```

# 15. Write a Way 2 (Script mode) Python script that takes an ordinary file in the current working directory as an argument, and removes the file from the file system if its size is zero bytes. Otherwise, the script should display the file's name, size, number of hard links, and inode number (in this order) on one line, with a header; similarly to what is shown in Example 16.25. Your script must do appropriate exception handling; for example, it should not work on hidden files or on files which are subdirectories in the current working directory.

# 16. Following Example 16.30, substitute your own selected directory name on your UNIX system as the source for backup, and back up all the files in that selected directory to