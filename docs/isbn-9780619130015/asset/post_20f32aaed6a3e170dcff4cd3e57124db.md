
4. Repeat the test command for the `phmenu`, `phoneadd` and `phlist1` files. After you confirm that these files exist, copy them to the source directory.

![](img/6d8286a85e2d8ad63e16f1801102da59_255_0.png)

> If you do not have the files from Chapter 6, see your instructor or technical support person for assistance.

5. If you permanently add the `/home/user-name/source` (where `user-name` is your login name) directory to your PATH variable, it takes effect each time you log on. You should do this in your `.bash_profile` file. Load the file into the vi editor. Your screen looks similar to Figure 7-15.

![](img/6d8286a85e2d8ad63e16f1801102da59_255_1.png)

6. Move the cursor to the line that reads:

```
PATH=$PATH:$HOME/bin
```

7. Type `i` to switch to insert mode. Type `:$HOME/source` (include the colon) at the end of the line.

8. Press `Esc`, then type `:wq` and press `Enter` to save the file and exit the editor.

9. To make the new PATH value take effect, you must log off and then log back on. Do so now.

You created the source directory and added it to your PATH variable. You can store your script files there and execute them just by typing their names at the command line. In the next exercise, you validate the existence of the `corp_phones` file.

### To validate the existence of a file:

- 1. Make sure you are in your source directory by typing `cd ~/source` and then pressing the **Enter** key.
- 2. Type `test -e corp_phones` and then press **Enter**.
- 3. Type `echo $?` and then press **Enter**. Your screen should show a “0,” which indicates a true status.

To see a demonstration of a false status, repeat the test for the file `phone_corp`, which does not exist.

Next you practice using the `test` command in a script file. Once again, recall the `os_choice` script you wrote in Chapter 6:

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

In the following exercise, you will modify the `if` statement so it uses the `test` command. When done, the program runs identically as it did before.

### To modify the if statement to use the test command:

- 1. Make sure you are in your home directory. Load the `os_choice` file into vi or Emacs.
- 2. Change the line that reads:
      `if [ "$OS_NAME" = "UNIX" ]`
      So it reads:
      `if test $OS_NAME = "UNIX"`
- 3. Save the file and exit the editor.
- 4. Test the script by executing it. Figure 7-16 shows sample output of the program.

![](img/6d8286a85e2d8ad63e16f1801102da59_257_0.png)

Figure 7-16: Output of updated os_choice script

In the next exercise, you modify a while loop so it uses the test command.

**To modify a while loop to use the test command:**

- 1. Recall the script named `colors`, which you wrote in Chapter 6. It repeatedly asks the user to guess its favorite color, until the user guesses the color red.

```bash
echo -n "Try to guess my favorite color "
read guess
while [ "$guess" != "red" ]; do
    echo "No, not that one. Try again. "; read guess
done
```

- 2. Load the file into vi or Emacs.
- 3. Change the line that reads:

```bash
while [ "$guess" != "red" ]; do
```

      So it reads:

```bash
while test $guess != "red" ; do
```

- 4. Save the file and exit the editor.

Test the script. Figure 7-17 shows sample output of the program.

![](img/6d8286a85e2d8ad63e16f1801102da59_258_0.png)

So far, you used the `test` command from both the command line and from within script files. You also configured your home directory structure and your PATH variable so you can run your script files directly from the source directory. Your next step is to begin enhancing the `corp_phones` program by formatting record output.

### Formatting Record Output

To format record output, use the `translate` utility. The **translate utility (`tr`)**, as you will recall from Chapter 5, changes the standard input (characters you type at the keyboard) character by character. The standard input can also be redirected with the `<` operator to come from a file rather than the keyboard. For example, the following command sends the contents of the `counters` file as input to the `tr` command. It converts lowercase characters to uppercase.

```
tr [a-z] [A-Z] < counters
```

By using the `|` operator, this command also works as a filter in cases where the input comes from the output of another UNIX command. For example, the following command sends the output of the `cat` command to `tr`:

```
cat names | tr -s ":" " "
```

This sample command sends the contents of the `names` file to `tr`. The `tr` utility replaces each occurrence of the `:` character with a space. The `tr` utility works like the `sed` command, except that `sed` changes the standard input string by string, not character by character.

You now use the `tr` utility to change lowercase characters to uppercase, as well as replace colon characters with spaces.

### To format using the grep and tr commands:

- 1. Use the `grep` command to retrieve a record from the `corp_phones` file that matches the phone number `219-555-4501`, and then pipe the output to `tr` to replace the colon characters in the record with space characters. Type the following command and then press `Enter`:

```
$ grep 219-555-4501 corp_phones | tr ':' ' '
```

      Your screen looks similar to Figure 7-18.

![](img/6d8286a85e2d8ad63e16f1801102da59_259_0.png)

Figure 7-18: Output of grep and tr commands

- 2. Change lowercase characters to uppercase in the `corp_phones` file by entering the following command and then pressing **Enter**:

```
$ cat corp_phones | tr '[a-z]' '[A-Z]'
```

      Your screen looks similar to Figure 7-19.

![](img/6d8286a85e2d8ad63e16f1801102da59_260_0.png)

Figure 7-19: Output of cat and tr commands

To search for phone numbers in the `corp_phones` file, your program can use techniques similar to those you executed in the steps above.

**To add record-searching capability to your program:**

- 1. The `phmenu` program is already equipped to call the script `phonefind` when the user selects `S` from the menu. This command instructs the program to search for a phone number. Use the vi or Emacs editor to create the `phonefind` program. Type the code shown:

```
#!/bin/bash
## Script Name: phonefind
## By: TEG
## Date: November 2000
## Purpose: Searches for a specified record in the
## corp_phones file
phonefile=~/source/corp_phones
clear
cursor 5 1
echo "Enter phone number to search for: "
cursor 5 35
read number
echo
grep $number $phonefile | tr ':' ' '
echo
echo "Press ENTER to continue..."
read continue
```

- 2. Save the file and exit the editor.
- 3. Use the `chmod` command to make the file executable, and then test the script by searching for the number `219-555-7175`. Your screen should look similar to Figure 7-20.

![](img/6d8286a85e2d8ad63e16f1801102da59_261_0.png)

Figure 7-20: Output of phonefind script

You formatted the record output of the program; your next task is to delete phone records.

### Deleting Phone Records

In this section you review the `sed` command. Recall from Chapter 5 that `sed` takes the contents of an input file and applies actions, provided as options and arguments, to the file's contents. The results are sent to the standard output device. A simple way to delete a phone record using `sed` is with the `d` (delete) option. Here is a pseudocode representation of the necessary steps:

- Enter phone number
- Use `sed -d` to delete the matching phone number and output to a temporary file, `f`
- Confirm acceptance
- If the output is accepted, copy the temporary file `f` back to `corp_phones` (overlaying it)

Now you revise the `phmenu` script to include the delete option.

**To delete phone records by editing the phmenu program:**

**1** Make sure you are in the source directory. Using the vi or Emacs editor, retrieve the revised `phmenu` program and add the code shown in boldface.

```
#!/bin/bash
#===============================================================
# Script Name: phmenu
# By: JQD
# Date: November 1999
# Purpose: A menu for the Corporate Phone List
# Command Line: phmenu
#===============================================================
phonefile=~/source/corp_phones
loop="y"
while test $loop = "y"
do
  clear
  cursor 3 12; echo "Corporate Phone Reporting Menu"
  cursor 4 12; echo "================================="
  cursor 6 9; echo "V - View Phone List"
  cursor 7 9; echo "P - Print Phone List"
  cursor 8 9; echo "A - Add Phone to List"
  cursor 9 9; echo "S - Search for Phone"
  cursor 10 9; echo "D - Delete Phone"
  cursor 12 9; echo "Q - Quit"
```
