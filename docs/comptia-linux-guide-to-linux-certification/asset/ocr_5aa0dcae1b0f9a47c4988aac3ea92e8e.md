20. Consider the following shell script:

```
echo -e "What is your favorite color?--> \c"
read REPLY
if [ "$REPLY" = "red" -o "$REPLY" = "blue" ]
then
echo "The answer is red or blue."
else
echo "The answer is not red nor blue."
fi
```

What would be displayed if a user executes the program in question 20 and answered **Blue** when prompted?

+   a. The answer is red or blue.

+   b. The answer is not red nor blue.

+   c. The code would cause an error.

+   d. The answer is red or blue. The answer is not red nor blue.

# Hands-on Projects

![](bbox=[0.1, 0.58, 0.25, 0.63])

These projects should be completed in the order given. The hands-on projects presented in this chapter should take a total of three hours to complete. The requirements for this lab include:

+   A computer with Fedora Linux installed according to Hands-on Project 2-1.

# Project 7-1

In this hands-on project, you use the shell to redirect the Standard Output and Standard Error to a file and take Standard Input from a file.

+   Boot your Fedora Linux virtual machine. After your Linux system has been loaded, switch to a command-line terminal (try2) by pressing **Ctrl+Alt+F2** and log in to the terminal using the user name of **root** and the password of **LNxRocks!**. 

+   At the command prompt, type `touch sample1 sample2` and press **Enter** to create two new files named sample1 and sample2 in your home directory. Verify their creation by typing `ls -F` at the command prompt, and press **Enter**. 

+   At the command prompt, type `ls -1 sample1 sample2 sample3` and press **Enter**. Is there any Standard Output displayed on the terminal screen? Is there any Standard Error displayed on the terminal screen? Why?

+   At the command prompt, type `ls -1 sample1 sample2 sample3 > file` and press **Enter**. Is there any Standard Output displayed on the terminal screen? Is there any Standard Error displayed on the terminal screen? Why?

+   At the command prompt, type `cat file` and press **Enter**. What are the contents of the file and why?

+   At the command prompt, type `ls -1 sample1 sample2 sample3 2>file` and press **Enter**. Is there any Standard Output displayed on the terminal screen? Is there any Standard Error displayed on the terminal screen? Why?