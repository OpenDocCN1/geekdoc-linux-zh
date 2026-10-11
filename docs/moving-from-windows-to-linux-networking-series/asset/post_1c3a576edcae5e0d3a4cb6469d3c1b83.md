
## System Variables

As we mentioned, a user-defined variable is, as its name suggests, a variable you create for some specific purpose in your script. You will find that most scripts of any complexity at all will require variables. The generic syntax for defining a user-defined variable is shown here: `variable name=value`

This means you provide some name for your variable, followed by an initial value to put in that variable. For example, you might have a variable that is designed to hold a person’s age. You would declare that in the following manner: `age=20`

Of course, you can store more than numbers in a variable. Perhaps you want a variable to store last names. You would declare that variable in this manner: `lastname=Smith`

You have a great deal of flexibility in naming variables, but there are some rules that must be obeyed. Variable names must begin with an alphanumeric character or underscore character (\_), followed by one or more alphanumeric characters. The following are all examples of valid variable names:
- `lastname`
- `_lastname`
- `variable7`

The second rule to remember regards the use of the equals sign (=) to assign values to your variables. You must remember to not put spaces on either side of the equals sign when assigning value to a variable. For example, the following variable declaration is correct: `no=20`

The following variable declarations are all in error:
- `age =20`
- `age= 20`
- `age = 20`

The third rule for you to remember is that variable names, like everything in Linux, are case sensitive. The following creates three variables named `age`, `Age`, and `AGE`, each with an initial value of 20.
- `age=20`
- `Age=20`
- `AGE=20`

This actually creates three variables named `age`, each with an initial value of 20.

The fourth rule regarding variable declaration regards null variables. A null variable is defined as one without any initial value. You can define a null variable by not assigning it any value after the equals sign, as you see here:
- `age=`
- `lastname=`

Creating a variable is not particularly difficult. Let’s examine a brief script that creates a couple of variables and prints their values to the screen.

```bash
#!/bin/bash
lastname=Easttom
firstname=Chuck
echo My name is $firstname $lastname
exit 0
```

Save this script as `scriptfive.sh` and run it from the shell. You should see what is shown in Figure 20.10.

![](img/12d790664598bbf390261087fbe55bbc_411_0.png)

**Figure 20.10**: Using variables.

Now we see how to create variables, but they will not be of much use unless we can do two things. The first is to put data in them. This will often be data from the user, so we need to explore how to get data from the user. We will also need to manipulate data arithmetically. Both topics will be examined in the next two portions of this chapter.

## Getting Input from the User

As was previously mentioned, variables will often get their values from user input. We need some method to take the data that the user types in at the keyboard and put it into the variables in our script. The vehicle for accomplishing this is the read statement. The read statement takes whatever is typed in, up to the point of the user pressing the Enter key, and puts that value into the designated variable. The following is an example of the syntax:

```bash
somevariable= 
read somevariable
```

Let's examine a script that has the user enter data and uses the echo statement to print the data to the screen. Type the following into your favorite text editor and save it as scriptsix.sh:

```bash
#! /bin/bash
lastname=smith
firstname=john
echo Please type in your first name
read firstname
echo Please type in your last name
read lastname
echo
echo Hello $firstname $lastname it is good to meet you.
exit 0
```

When you run this script you should see something similar to what is shown in Figure 20.11, although your display will vary, of course, depending on the name you enter.

![](img/12d790664598bbf390261087fbe55bbc_412_0.png)

**Figure 20.11**: Getting user input.

You see this is a rather friendly script! It also demonstrates how to create a variable and how to fill that variable with data the user provides. Notice that when we display the values of the variables to the screen, we get the values the user typed in, not the initial values we put in our script. The contents of the variables were overwritten by the data the user entered. If you will recall, we stated earlier that they are called variables because their content can vary.

## Math in Scripts

In addition to getting input from the user, you often will want to perform some basic arithmetic operations. This is a place where scripts can be particularly useful. If you have some calculations you need to perform on a regular basis, you can use a script to automate that task. The generic syntax used is this:

```bash
expr operator1 math-operator op2
```

For example, you can add two numbers by typing in

```bash
expr 20 +2
```

The math you can do in a Linux shell script is very limited. Essentially you can do very simple arithmetic operations on two operators. One or both of the operators can be a variable, so you could write a script that asks the user for two numbers and adds or subtracts them. For more advanced math you will need a more advanced scripting language, and that is beyond the scope of this book. However, let’s take a moment to look at a script that does use the limited math capabilities available. Type the following into the text editor of your choice and save it as scriptseven.sh:

```bash
#!/bin/bash
numone=0
numtwo=0
echo Please enter the first number
read numone
echo Please enter the second number
read numtwo
echo $numone added to $numtwo is `expr $numone + $numtwo`
exit 0
```

When you run this script, you should see something much like what is displayed in Figure 20.12.

![](img/12d790664598bbf390261087fbe55bbc_413_0.png)

Admittedly this is not particularly advanced math or even very interesting! But it does illustrate the very basic arithmetic capabilities of a Linux shell script. You may have noticed what appear to be single quotes on each side of the expr $numone + $numtwo statement. These are not actually single quotes, they are backquotes. On most keyboards, to the left of the number one key, you will see a key that has a `~` and a `` ` `` mark. The first is called a tilde, and the second is the backquote. It is imperative that you use the backquote rather than the single quote that is to the right of your colon/semicolon key.

## if Statements in Scripts

In any programming or scripting language, you need to take alternative actions depending on some input. If some condition is true, then execute one set of code, and if it's not, execute a different set. The following is a generic example of the syntax used:

```bash
if condition
then
    # condition is zero (true - 0)
    # execute these commands

else
    # if condition is not true then
    # execute these commands
fi
```

> **Note**: `fi` indicates a finished `if` statement.

Let's look at a script that illustrates this. In your favorite text editor, enter the following lines and save it as `scripteight.sh`:

```bash
#!/bin/bash
num=0
echo Please enter an integer
read num
if test $num -gt 0
then
    echo $num is positive
else
    echo $num is a negative number
fi
exit 0
```

If you run this script from the shell, you should see something similar to what is displayed in Figure 20.13.

![](img/12d790664598bbf390261087fbe55bbc_414_0.png)

There are several items in this particular script that we need to pay attention to. The first line that is different from what we have previously seen is `if test $num -gt 0`. This line says to see if the variable `num` is greater than (gt) zero. If it is, then proceed to the code found under the `then` statement. If it is not, then proceed to the code found under the `else` statement. Complete the `if` with the `fi` statement.

The `if` statement is a construct that is common to virtually all scripting and programming languages. Whether you are doing a Linux shell script, a Windows batch file, a JavaScript, or a C++ program, you will have `if` statements that follow essentially the same structure as you see here. The syntax will be a bit different from one language to the next, but the basic structure is essentially the same.

You also can have an entire `if` statement, including the `fi`, inside of another `if` statement. These are referred to as **nested `if`** statements. If you think about this for a moment, it's not so strange. You use nested `if` statements in your day-to-day thinking. For example, before going to work in the morning, you might say to yourself that if the freeway is busy, take a side route. Then if the freeway is busy, you
