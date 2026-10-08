Note: Throughout the sample scripts, variables are always enclosed in double quotes, as in “$choice,” “$looperst,” “$yesno,” “$guess,” and “$myfavorite,” due to how the shell interprets variables. All shell variables, unless declared otherwise, are strings, which are arrays of characters. If you do not enter data in the string variables, the variables will be treated as blank strings, which result in an invalid test. The enclosing double quotes therefore maintain the validity of strings, with or without data, and the test is carried out without producing an error condition.

# To demonstrate decision logic:

+   1. Type **vi os_choice** and press **Enter**.
2. Type **i** to switch to vi's insert mode.
3. Type the following lines:

```
```bash
echo -n "What is your favorite operating system? "
read OS_NAME
if [ "$OS_NAME" = "UNIX" ]
then
    echo "You will like Linux."
else
    echo "You should give Linux a try!"
fi
```
```

+   4. Press **Esc** to switch to vi’s command mode.
5. Type **:wq** and press **Enter** to save the file and exit vi.

Before you run the program, let's examine its contents. The first statement uses the echo command to display a message on the screen. The -n option suppresses the line feed that normally appears after the message. The second statement uses the read command, which waits for the user to type a line of keyboard input. The input is stored in the variable specified as the read command's argument. The line in the program reads the user's input into the OS_NAME variable.

The next line begins an if statement. The word “if” is followed by an expression inside a set of brackets ([ ]). (The spaces that separate the [ and ] characters from the enclosed expression are necessary.) The expression, which is tested to determine if it is true or false, compares the contents of the OS_NAME variable with the string UNIX. (When you use the = operator in an if statement's test expression, it tests its two operands for equality. If the operands are equal, the expression is true. Otherwise, it is false.) If the contents of the OS_NAME variable is equal to UNIX, the statement that follows the word “then” is executed. In this program, it is an echo statement.

If the if statement's expression is false (if the contents of the OS_NAME variable does not equal UNIX), the statement that follows the word “else” is executed. In this program, it is a different echo statement.

Notice the last statement, which is the word fi. fi (“if” spelled backward) always marks the end of an if or an if...else statement.