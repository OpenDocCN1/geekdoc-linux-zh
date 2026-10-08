You created the source directory and added it to your PATH variable. You can store your script files there and execute them just by typing their names at the command line. In the next exercise, you validate the existence of the corp_phones file.

# To validate the existence of a file:

+   1. Make sure you are in your source directory by typing `cd ~/source` and then pressing the **Enter** key.
2. Type `test -e corp_phones` and then press **Enter**.
3. Type `echo $?` and then press **Enter**. Your screen should show a “0,” which indicates a true status.

To see a demonstration of a false status, repeat the test for the file phone_corp, which does not exist.

Next you practice using the test command in a script file. Once again, recall the os_choice script you wrote in Chapter 6:

```
echo -n "What is your favorite operating system? "
read OS_NAME
if [ "$OS_NAME" = "UNIX" ]
then
    echo "You will like Linux."
else
    echo "You should give Linux a try!"
fi
```

In the following exercise, you will modify the if statement so it uses the test command. When done, the program runs identically as it did before.

# To modify the if statement to use the test command:

+   1. Make sure you are in your home directory. Load the os_choice file into vi or Emacs.
2. Change the line that reads:
   `if [ "$OS_NAME" = "UNIX" ]`
   So it reads:
   `if test $OS_NAME = "UNIX"`
3. Save the file and exit the editor.
4. Test the script by executing it. Figure 7-16 shows sample output of the program.