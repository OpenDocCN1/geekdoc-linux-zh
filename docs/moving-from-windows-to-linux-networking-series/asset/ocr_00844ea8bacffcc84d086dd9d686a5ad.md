# System Variables

As we mentioned, a user-defined variable is, as its name suggests, a variable you create for some specific purpose in your script. You will find that most scripts of any complexity at all will require variables. The generic syntax for defining a user-defined variable is shown here: `variable name=value`

This means you provide some name for your variable, followed by an initial value to put in that variable. For example, you might have a variable that is designed to hold a person’s age. You would declare that in the following manner: `age=20`

Of course, you can store more than numbers in a variable. Perhaps you want a variable to store last names. You would declare that variable in this manner: `lastname=Smith`

You have a great deal of flexibility in naming variables, but there are some rules that must be obeyed. Variable names must begin with an alphanumeric character or underscore character (\_), followed by one or more alphanumeric characters. The following are all examples of valid variable names:
`lastname`
`_lastname`
`variable7`

The second rule to remember regards the use of the equals sign (=) to assign values to your variables. You must remember to not put spaces on either side of the equals sign when assigning value to a variable. For example, the following variable declaration is correct: `no=20`

The following variable declarations are all in error:
`age =20`
`age= 20`
`age = 20`

The third rule for you to remember is that variable names, like everything in Linux, are case sensitive. The following creates three variables named `age`, `Age`, and `AGE`, each with an initial value of 20.
`age=20`
`Age=20`
`AGE=20`

This actually creates three variables named `age`, each with an initial value of 20.

The fourth rule regarding variable declaration regards null variables. A null variable is defined as one without any initial value. You can define a null variable by not assigning it any value after the equals sign, as you see here:
`age=`
`lastname=`

Creating a variable is not particularly difficult. Let’s examine a brief script that creates a couple of variables and prints their values to the screen.

```
```
#!/bin/bash
lastname=Easttom
firstname=Chuck
echo My name is $firstname $lastname
exit 0
```
```

Save this script as `scriptfive.sh` and run it from the shell. You should see what is shown in Figure 20.10.