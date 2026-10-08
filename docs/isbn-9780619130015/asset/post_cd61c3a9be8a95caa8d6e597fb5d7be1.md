
In the Manycolors script, the case structure examines the contents of the color variable and searches for a match among the values listed. When a match is found, the statement that immediately follows the case value is executed. For example, if the color variable contains red, the echo statement that appears after "red") is executed. If the contents of the colors variable does not match any of the values listed, the statement that appears after \*) is executed.

As you can see, case logic is designed to pick one course of action from a list of many, depending upon the contents of a variable. This control structure is ideal for menus, where the user chooses one of several values.

Note: The case structure is terminated by the word "esac," which is "case" spelled backwards.

In this section, you learned about shell variables, operators, and wildcard characters. You also learned about the four logic structures. In the next section, you’ll use shell programming to create your application.

## SUMMARY

- A high-level language (such as C, C++, or COBOL) is a language that uses English-like expressions. A high-level language must be converted into a low-level (machine) language before the computer can execute it.
- The shell interprets UNIX shell scripts. They do not need to be converted to machine language because UNIX converts and executes them in one step.
- UNIX shell scripts, created with the vi or Emacs editor, contain instructions that do not need to be written from scratch, but rather can be selectively chosen from the operating system’s inventory of executable commands.
- Linux shells are derived from the UNIX Bourne, Korn, and C shells. The three Linux shells are Bash, tesh, and zsh; Bash is the most used Linux shell.
- UNIX keeps three types of variables: configuration, environment, and shell. Configuration variables contain set-up information for the operating system. Environment variables keep information about your login session. Shell variables are created in a shell script or at the command line. The export command is used to make a shell variable an environment variable.
- The shell supports numerous operators, including many for performing arithmetic operations.
- You can use wildcard characters in shell scripts, including the bracket ([]) characters. Brackets surround a set of values that can match an individual character in a name or string.
- The logic structures supported by the shell are sequential, decision, looping, and case.

## REVIEW QUESTIONS

1. Shell programs ______________________.
   - a. can be developed faster than compiled programs
   - b. run slower than their compiled counterparts
   - c. serve as excellent prototypes
   - d. All of the above

2. What is the difference between a configuration variable and an environment variable?
   - a. The user sets configuration variables.
   - b. The system sets environment variables.
   - c. The system sets configuration variables.
   - d. The user should never change environment variables.

3. Which of the following commands protect a file from being overwritten?
   - a. set -o noclobber
   - b. chmod 777 *filename*
   - c. set -o clobber
   - d. set !*filename*

4. The four basic logic structures are ______________________.
   - a. sequence, decision, loop, and case
   - b. sequence, iteration, loop, and case
   - c. decision, iteration, case, and if-then
   - d. for, next, while, and if

5. Which of these commands stores the output of the date command in the variable MYDATE?
   - a. MYDATE=date
   - b. date > MYDATE
   - c. MYDATE=`date`
   - d. date | MYDATE

6. The program development cycle can be described as ______________________.
   - a. program design, program specifications, writing code, testing and debugging
   - b. program specifications, program design, writing code, testing and debugging
   - c. writing code, testing and debugging, program design, program specifications
   - d. program design, writing code, testing and debugging, program specifications

7. The ______________________ command displays a list of environment variables.
   - a. printenv
   - b. envs
   - c. ls-env
   - d. cat envs

8. The ______________________ command makes a variable an environment variable.
   - a. send
   - b. port
   - c. export
   - d. import

9. Sequential logic can be described as ______________________.
   - a. a logic structure for executing a statement or group of statements only if a certain condition exists
   - b. a logic structure for executing a series of statements in the order they are written
   - c. a logic structure for repeating a statement or series of statements
   - d. a logic structure for performing one of many actions, depending upon the value of a variable

10. Decision logic can be described as ______________________.
    - a. a logic structure for executing a statement or group of statements only if a certain condition exists
    - b. a logic structure for executing a series of statements in the order they are written
    - c. a logic structure for repeating a statement or series of statements
    - d. a logic structure for performing one of many actions, depending upon the value of a variable

11. Looping logic can be described as ______________________.
    - a. a logic structure for executing a statement or group of statements only if a certain condition exists
    - b. a logic structure for executing a series of statements in the order they are written
    - c. a logic structure for repeating a statement or series of statements
    - d. a logic structure for performing one of many actions, depending upon the value of a variable

12. Case logic can be described as ______________________.
    - a. a logic structure for executing a statement or group of statements only if a certain condition exists
    - b. a logic structure for executing a series of statements in the order they are written
    - c. a logic structure for repeating a statement or series of statements
    - d. a logic structure for performing one of many actions, depending upon the value of a variable

13. The ______________________ command stores the user's input in a variable.
    - a. input
    - b. get
    - c. read
    - d. import

14. Shell programs are ______________________.
    - a. compiled
    - b. interpreted
    - c. both compiled and interpreted
    - d. neither compiled nor interpreted

## EXERCISES

1. Create the file alphalist with the following entries:
    Alpha_romeo
    Chevrolet
    Buick
    Plymouth
    Dodge
    BMW

2. Sort the alphalist file and pipe it to a cat program to display a numbered list of cars.

3. Create a new file, myfile, in your home directory.
   - a. Use the set -o noclobber. Create a second file, mynewfile.
   - b. Enter this command: cat mynewfile > myfile <Enter>.
   - c. Explain what happened.
   - d. Now modify the redirection to make it work.

4. Fix this line of code to make it work:
   ```bash
   echo “Why don’t you get a “van down by the river?”
   ```

5. If you do not have a bin directory in your home directory, create one. Look at the contents of the PATH variable. If it does not include the path to your bin directory, add it.

6. Create a variable, NAME. Store your full name in it.

7. Use the printenv command to display a list of environment variables. Is the NAME variable listed? Execute the command that makes NAME an environment variable.

## DISCOVERY EXERCISES

1. Use the sample menu as a guide, and create a new menu program that looks like this:
   Travel Menu
   ===========
   (L)ondon scenic tour
   (P)aris in the Spring
   (N)ew York Shopping Fantasy
   Make your selection ... (Q) to quit

2. Enter the command to store the output of the pwd command in a variable, PLACE. Display the contents of the PLACE variable on the screen.

3. Write a script named change_prompt. The script should change your prompt to display the date and the name of your working directory. Give the file execute permission, and test it.
