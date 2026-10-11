
## Part II: The Basics of Writing Code

Sometimes strings consist of numbers instead of letters, but they’re still strings, such as in the following telephone number:

```
declare Telephone="555-5555"
```

Don’t forget this rule: Put quotation marks around a string value. Quotation marks tell Linux that characters appearing between the quotation marks belong together and that it’s to treat them as a string.

### Assigning variables to other variables

You can take data that you stuff into one variable and copy it to another variable. You end up with two copies of the data. Your computer doesn’t remove the data from the original variable.

The following example shows you how to copy data from one variable to another by using a string variable:

```
declare MyGoal="Buy out Bill Gates"
declare OurGoal="$MyGoal"
```

In this example, you’re telling your computer in the first line to go to the variable MyGoal and copy the data that’s there. Next, you’re telling your computer to take that data and place it into the variable OurGoal. You’re doing so by using the name of the original variable, and you’re placing a dollar sign ($) in front of it.

You can perform this same copying procedure by using a numeric variable, as in the following example:

```
let MySalary=1000000
let OurSalaries=$MySalary
```

Your computer takes a copy of the value of your salary and stuffs it into the variable OurSalaries. The value of OurSalaries is now the same as your salary, 1000000. Your own million-dollar salary, however, remains safe in the MySalary variable.

### Using Data Types

A Linux variable can store any number or string. You can confuse your computer, however, if you first tell it one thing and then tell it to do something completely opposite (and computers don’t like you confusing them).

Say, for example, that you ask your computer to find a place to stuff someone's name (that is, to create a variable). But as the time arrives to do the actual stuffing, you give it the person's salary instead.

Your computer turns around and says something like “Hey — what goes on? First you tell me that you want to store a string. Okay, so I do all this work and find the perfect spot for your string. Now you give me a number. I have no room for the number there.” What’s more embarrassing is if it’s someone else’s computer that complains — which means that everyone who uses your program knows that you goofed.

Whenever you declare a variable, you specify the *data type* of the variable. Some computer languages use many data types to handle all sizes of numbers and strings. But don't concern yourself with all these choices. Linux uses just the following two data types:

- Numeric data type
- String data type

Make sure that you check the data type of the variable in your program before you assign it a value. That way, you don't give your computer a reason to complain about your program.

### The Scope of Variables

The *scope* of a variable determines who can use the variable within Linux. You can tell Linux who can access a variable two ways: by using *local* and *environment* variables.

Only the program that creates it can use a *local variable*. This property of a local variable helps you isolate your information from anything else that's running on your computer. The following example shows you how to declare a local variable within your program:

```
declare SSNum
let Salary=1000000
```

But what if you want to share this information with other programs? In that case, you must declare the variable as an *environment variable*. Any program that's running on your computer can read a global variable and change the value of the environment variable.

In many computer languages, such as the Java language, you create a *global variable* by putting it in a special place in your program file. But you don't declare a global variable in Linux that way. Instead, you use the `export` keyword, which creates an environment variable. As is true of a global variable, you can share an environment variable with other programs.

The following example shows you how to declare a global variable within your program (so just follow this example so that the entire world can know your Social Security number):

```
declare SSNum="555-55-5555"
```

You must be very careful whenever you decide to use a global variable in your program for the following reasons:

- Any program running on the same computer as your program can read and change the value that you store in the global variable.
- The last value that you assign to the global variable is the one that your computer keeps. So if two programs change the value of the same global variable, one program may not work correctly.
- Finding a problem resulting from someone assigning a wrong value to a global variable can become a nightmare. You don't know which program changed it.

## Chapter 5

## Interfacing with the User

In This Chapter

- Getting data from the keyboard input
- Displaying data that the user enters
- Keeping your data in a file

The part of the program that the user sees — the *user interface* — is like window dressing for your program. It makes your program look pretty. A pretty user interface, however, doesn’t necessarily help someone do something with your program.

If you want your program to be more useful than just a pretty picture on-screen, you need it to interact with the user. Your program must carry out the following tasks to interact with the user:

- Get information from the user (via the keyboard).
- Do something with that information.
- Show the results of what it does with the information on the user interface.

In this chapter, I show you the command that tells your program to read information that someone enters from the keyboard. Then I show you how to display that information on-screen.

### Keyboard Input

The user interface displays messages (known as *prompts*) on-screen, and these messages tell someone to press a key on the keyboard — but your program can’t *force* the user to press a key. Your interface is all you have to entice the user into doing what you want.

### Pretty Linux

Mr. Gates finally gave DOS a makeover, and it came out looking like Windows. Linux, however, is still undergoing its makeover. The first improvement enables a user to open more than one window on-screen. To do so, the user needs special software known as X Windows. The next improvement involves jazzing up those windows with push buttons, drop-down lists, and all those things that Windows machines and Macs display. You need additional special software for this improvement. That software is known as Motif. So unless you intend to find out how to build your program so that you can use X Windows and Motif with it, you must live with a basic program that doesn't use the windowing features you see on Windows and Mac.

You can't write a pretty user interface for Linux like you see in Macs and PCs running Windows programs unless you know how to program X Windows and Motif (see Chapter 1). Linux is a plain-Jane operating system, like DOS. Expect your program only to wait patiently until someone presses the Enter key after typing each piece of information. In the meantime, your computer's collecting and storing all the keystrokes somewhere inside it that's known as a *keyboard buffer*. After the user presses the Enter key, your program rushes to grab all those characters that the user entered at the keyboard and stuff them into the variables that you created for them.

### Reading a string

Your computer isn't too bright whenever it must pick up data from the keyboard. (But, on the other hand, it would like to use *us* find the square root of 365 in less than a second.) Your computer doesn't know whether to treat a number as a character or a value to use in a calculation. It finds out only after you specify the kind of variable that you want to use to store the information.

After you tell the computer the correct variable to use, you must tell it to read the characters from the keyboard. The following code shows you how to tell the computer to read characters and then stuff them into a string variable:

```
#!/bin/bash
clear
echo
echo "Enter Your First Name: "
read FirstName
```

First, `#!/bin/bash` tells the computer to start the *bash* shell before clearing (clear) the screen.
