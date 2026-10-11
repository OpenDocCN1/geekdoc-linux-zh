
## Accepting Arguments

You can also pass information to a subprogram. You call a subprogram from within a program or from another subprogram by using the following command (displaymenu being the name of the subprogram):

```bash
displaymenu
```

> Notice that the $ sign is missing. It doesn't appear because you're calling the subprogram from within another program. The $ sign appears only if you start the program from the command line.

You can send data to a subprogram the same way that you send data to a program from the command line, as the following example shows:

```bash
displaymenu yes
```

> Following are some rules to go by in sending data to a program from the command line:
>
> - Place a space between the name of the program and the data.
> - Place a space between each data item if you're sending multiple data to the program. See the section "Passing Multiple Arguments," later in this chapter, for more of the lowdown on multiple data.

Well, if you can pass information to your program (or subprogram), you must write instructions in your program (or subprogram) to do something with the information after it receives it. This activity that the program performs is commonly known as accepting arguments.

Linux stores the information that it passes to your program in a variable by the name of $1. The number 1 tells your program that you want to refer to the first piece of information that passes to the program. (As you see in the section "Passing Multiple Arguments," later in this chapter, you can pass more than one piece of information to the program.) To refer to this information, for example, you type the following code at the command line:

```bash
$1
```

If your program is the one that's getting you a snack from the kitchen, giving it this information is like telling it what kind of snack you want. You write something such as the following line:

```bash
getsnack chips
```

The program sees *chips* as the value that you assign to the $1 variable. The program just goes about its business, using $1 whenever it needs to refer to the snack that you want from the kitchen.

Now, you need to get real and take a look at a practical way of using this information. In the following example, I do something sneaky. I create a displaymenu program that displays a menu, receives a response from the user, and then executes the appropriate subprogram. This program, however, displays the menu and does all the other stuff only if you pass the magic word—*yes*—to the program. Otherwise the program skips directly to the end of the program without showing anything on-screen.

> Your program can do more than just display the data item it receives. Sometimes your computer uses the data as the criteria to make a decision.

The following example shows you how I set up the displaymenu program that I mention a couple paragraphs earlier:

```bash
#!/bin/bash

if [ "$1" -eq "yes" ]
then
clear
echo "Telephone Directory"
echo
echo "1. Find Listing"
echo "2. Add Listing"
echo "3. Modify Listing"
echo "4. Print Listing"
echo "0. Quit"
echo
read selection
case $selection in
    "1") findlisting ; ;
    "2") addlisting ; ;
    "3") modifylisting ; ;
    "4") printlisting ; ;
    "0")     exit
    esac
fi
```

This example is an involved version of the displaymenu program, because the program is receiving information from the command line. The menu appears only if the user sends the program a magic word. (The magic word is *yes*.) The following steps describe what happens in a nutshell:

1. The computer starts the `bash` shell.
2. The program compares the data the user sends it to the word `yes`.
3. If the data and the magic word match, the menu appears and the computer does something after the user makes a selection.
4. If the data and the magic word don't match, the program ends.

## Passing Multiple Arguments

A program can pass your program (or subprogram) more than one argument from the command line. This capability becomes very useful whenever your program requires more than one piece of information to perform a task.

Say that you write a program that displays names on-screen — names of your friends. If you write the program to accept these names from the command line, you can place each name on the command line, making sure that you separate each one with a space. The space character enables your program to recognize where one piece of information begins and the other ends. Take a glance at the following example:

```bash
$ displayfriends Bob Mary Joe Sue
```

Each piece of information must appear to the right of the program name. A space must separate each data item.

Your program can use this information by using the $1 variable (which I explain in the preceding section) with the corresponding number of the data item, as in the following example:

```bash
#!/bin/bash  
echo "My friend $1"  
echo "My friend $2"  
echo "My friend $3"  
echo "My friend $4"
```

This program shows the names of your friends on-screen, as follows:

```bash
My friend Bob  
My friend Mary  
My friend Joe  
My friend Sue
```

![](img/05279073f26be7df99b3c487360dec6a_187_0.png)

> Knowing how to pass multiple arguments to your program and subprograms provides flexibility to your programming. You no longer must write into the code all the information that your program requires. Nor do you need to constantly prompt the user for information. Instead, you can simply enter the information on the command line or as your program calls a subprogram, and the information passes to the program or subprogram.

## Problems with Sending Arguments

![](img/05279073f26be7df99b3c487360dec6a_188_0.png)

Two common problems can occur whenever anyone sends your program or subprogram arguments: Someone can send you the wrong number of arguments or the wrong kind of arguments.

### The wrong number of arguments

You can plan to receive a fixed number of arguments, but nothing forces someone to send you the correct number. Suppose that your program expects the following two arguments:

```bash
#!/bin/bash
echo "First Name: $1"
echo "Last Name: $2"
```

Now suppose that someone supplies only one of those arguments, as follows:

```bash
$ displayname Bob
```

Your program is still telling your computer to use the second data item that it expects to pass to the program — in this case, the phantom data.

### The wrong kind of argument

Your program depends on someone else to pass it the correct information. If this person isn't dependable, your program experiences problems. Say that someone calls your program and sends the following information:

```bash
$ nanegame car: truck
```

Your program assumes that the information is just what it's looking for in the following example:

```bash
#!/bin/bash
echo "First Name: $1"
echo "Last Name: $2"
```

But that information isn't what your program expects and your program is using incorrect information. So who's going to get the blame for the problem? The person using your program or the programmer? (Who, you? Why, it's not your fault . . . is it?) You have no easy way to avoid this situation or the blame (except by not answering the phone if the user calls to complain). As long as you note in the documentation of your program that the user needs to enter specific kinds of information at the command prompt as the program runs, your job is done. You can't force the user to read the documentation before running your program. But you still hear such excuses as “Of course I … didn’t … read the instructions.”

## Does Your Argument Exist?

Your program sometimes needs for someone to send data to it; otherwise, your program can't perform the task. So the first thing that your program needs to do is to determine whether anyone's sending any data to it.

You can use the $\$ variable to determine the number of data items that your program receives. The $* variable contains the number of arguments that pass to your program. Notice the difference between $1, which you use to reference an argument, and $# , which just contains the number of arguments that your program receives.

The following example shows you how you use the $# variable:

```bash
#!/bin/bash
echo "$#"
```

This program displays the number of data items it’s receiving. As you run this program, you don’t see the data itself; instead, you see a number on-screen, which represents the number of data items your program is receiving.

You can compare the value of $# with the number of data items that your program requires by using the following example:

```bash
#!/bin/bash
if [ "$#" -eq 2 ]
then
    echo "You entered the correct number of arguments."
else
    echo "You didn't enter the correct number of arguments."
fi
```

In the preceding code, the program starts the bash shell and then determines whether the correct number of arguments pass to the program. In this case, I decide that two arguments are necessary, basing my decision on the specifications for the program.

So the program uses the if statement to compare the value in $# with the value 2. If it finds a match, the program displays a message and continues (although I don't show the rest of the program in this example). If it doesn't find a match, the program ends.
