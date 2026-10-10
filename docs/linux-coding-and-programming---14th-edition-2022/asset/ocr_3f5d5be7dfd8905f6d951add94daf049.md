# **STEP 5**
When you run the script now you can use two custom variables: `./hello.sh David Hayward`. Naturally change the two variables with your own name; unless you’re also called David Hayward. At the moment we’re just printing the contents, so let’s expand the two-variable use a little.

![](bbox=[0.06, 0.215, 0.49, 0.32])

# **STEP 6**
Create a new script called `addition.sh`, using the same format as the hello.sh script, but changing the variable names. Here we’ve added `firstnumber` and `secondnumber`, and changed the echo command to output some simple arithmetic by placing an integer expression, `echo $((($firstnumber+$secondnumber)))`. Save the script, and make it executable (`chmod +x addition.sh`).

![](bbox=[0.06, 0.52, 0.49, 0.645])

# **STEP 7**
When you now run the addition.sh script we can enter two numbers: `./addition.sh 1 2`. The result will hopefully be 3, with the terminal displaying ‘The sum is 3’. Try it with a few different numbers and see what happens. See also if you can alter the script and rename it do multiplication, and subtraction.

![](bbox=[0.06, 0.79, 0.49, 0.91])

# **STEP 8**
Let’s expand things further. Create a new script called `greetings.sh`. Enter the scripting as below in the screenshot, save it and make it executable with the `chmod` command. You can see that there are a few new additions to the script now.

![](bbox=[0.51, 0.215, 0.95, 0.32])

# **STEP 9**
We’ve added a `-n` to the echo command here which will leave the cursor on the same line as the question, instead of a new line. The `read` command stores the user’s input as the variables `firstname` and `surname`, to then read back later in the last echo line. And the `Clear` command clears the screen.

![](bbox=[0.51, 0.52, 0.95, 0.645])

# **STEP 10**
As a final addition, let’s include the date variable we used in the last section. Amend the last line of the script to read: `echo Hello $firstname $surname, how are you on this fine day $(date +%A)?`. The output should display the current day of the week, calling it from a system variable.

![](bbox=[0.51, 0.79, 0.95, 0.91])