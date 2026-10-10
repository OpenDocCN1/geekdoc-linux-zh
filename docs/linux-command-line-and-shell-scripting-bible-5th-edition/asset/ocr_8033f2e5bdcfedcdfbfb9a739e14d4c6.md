```
echo -e "\t3. Display memory usage"
echo -e "*\t0. Exit menu\n"
echo -en "\t\tEnter option: "
```

The -en option on the last line displays the line without adding the newline character at the end. This gives the menu a more professional look, because the cursor stays at the end of the line waiting for the user's input.

The last part of creating the menu is to retrieve the input from the user. This is done using the read command (see Chapter 14, “Handling User Input”). Because you are expecting only single-character input, the nice thing to do is to use the -n option in the read command to retrieve only one character. Doing so allows the user to enter a number without having to press the Enter key:
read -n 1 option
Next, you need to create your menu functions.

# Create the menu functions

Shell script menu options are easier to create as a group of separate functions. This approach enables you to create a simple, concise case command that is easy to follow.

To do that, you must create separate shell functions for each of your menu options. The first step in creating a menu shell script is to determine what functions you want your script to perform and lay them out as separate functions in your code.

It is common practice to create stub functions for functions that aren't implemented yet. A stub function is a function that doesn't contain any commands yet or possibly just an echo statement indicating what should be there eventually:

```
function diskspace {
    clear
    echo "This is where the diskspace commands will go"
}
```

The stub function enables your menu to operate smoothly while you work on the individual functions. You don't have to code all the functions for your menu to work. You'll notice that the function starts with the clear command. This enables you to start the function on a clean monitor screen, without the menu showing.

One thing that helps out in the shell script menu is to create the menu layout itself as a function:

```
function menu {
    clear
    echo
    echo -e "*\t\tSys Admin Menu\n"
    echo -e "*\t1. Display disk space"
    echo -e "*\t2. Display logged on users"
    echo -e "*\t3. Display memory usage"
    echo -e "*\t0. Exit program\n"
```