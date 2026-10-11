
You insert the name of the subprogram as an instruction into your program the same way that you place the other instructions into your program. In fact, you can write a program that contains only one instruction — the name of a subprogram. The following example shows how such a program looks:

```bash
#!/bin/bash
displaymenu
```

Not much to this program. It simply starts the **bash** shell and then calls the **displaymenu** subprogram. The subprogram does all the work in this case. The **displaymenu** subprogram displays a menu on-screen.

You can build large, complex programs from many subprograms. And sometimes you can reuse subprograms in other programs without even modifying the subprogram. Suppose, for example, that you create a subprogram that prompts the user to enter a name and password and then validates the password. You can use this same subprogram with other programs that also need this task.

## Sharing Subprograms

Don’t throw away the subprograms that you build! Programmers treat their collection of subprograms almost as collector’s items. A subprogram that’s working smoothly is worth its weight in gold. Okay, maybe it’s not *that* valuable yet. But a programmer who can choose between building a subprogram from scratch or getting one from a friend always opts for the latter.

But don’t go looking for a formal trading post where you can exchange subprograms. You really aren’t going to find any. You can, however, post your request for subprograms on the appropriate newsgroups on the Internet (see Chapter 21 for details). You can also ask other programmers that you meet whether they have any good subprograms that you can take a peek at.

# Chapter 15

## Understanding Arguments . . . Not the Ones with Your Mother-in-Law

### In This Chapter

- Arguments, arguments, arguments
- Passing arguments
- Accepting arguments
- Avoiding problems with arguments
- Checking your arguments

Here's a good excuse to use the next time that you want to argue with your significant other: Just say, "I'm not arguing; I'm simply passing you information." Feel free to use this expression (but don't attribute it to me).

Most of us think of an argument as words of disagreement that can heat up and sometimes lead to blows. But to your computer, an argument is information that goes to a program (or subprogram) from the command line after the program (or subprogram) executes.

### Using Arguments — Why?

![](img/05279073f26be7df99b3c487360dec6a_182_0.png)

The capability to pass arguments enables you to build flexible programs and subprograms. Remember that a program can really consist of a group of subprograms. Each subprogram performs one task very well. After you build a subprogram and get it running smoothly, you don't need to modify the instructions within the subprogram. (If it ain't broke, don't fix it.)

The best way to use information between the program and subprogram is to pass the specific data to the subprogram as an argument on the command line. Although you don't fool with the "innards" of a subprogram, you enable the subprogram to share the information that pertains to your current program.

Say that you build a subprogram to fetch you snacks from the kitchen (just dreaming). The subprogram is all ready to do the legwork for you. But the subprogram needs to know what snacks you want. How can you give it this information? Well, as you call the subprogram, you use the command line to pass it the name of the snack. If you write the subprogram to receive the snack information, you can just sit back in your recliner and keep surfing the tube.

Although I say that you pass arguments from the command line to the program (or subprogram), you can also pass arguments to the programs (or subprograms) from within your program by typing the name of the program (or subprogram) and following it with the argument.

![](img/05279073f26be7df99b3c487360dec6a_183_0.png)

Passing an argument to a program (or subprogram) is different from the way that I show you to write programs in earlier chapters. In all the programs that you create in the preceding chapters of this book, you always provide to your program the information directly into the program. Every time that you want to change the data — if, for example, you need to change "Bob" to "Robert" — you must change the program.

```bash
declare FirstName="Bob"
```

In the preceding line of code, you assign the name `Bob` to the string variable `FirstName`. This type of assignment is known as **hard coding** the information into the program. Hard coding is a term that programmers use to say that you type the information directly into the program. Every time that you want to change the data — if, for example, you need to change "Bob" to "Robert" — you must change the program.

In Chapter 5, you see another way that a program gathers information: It can ask the user to enter the information while the program’s running, as in the following example:

```bash
declare FirstName
echo "Enter your first name: "
read FirstName
```

Here, the program asks the user to enter his first name. The program then assigns the name to the string variable `FirstName`. The information that the user enters changes every time that the program runs, without the programmer needing to change anything inside the program.

Hard coding information is not always the best way to get information into your program, because the programmer needs to change that program each time that the information changes.

![](img/05279073f26be7df99b3c487360dec6a_183_1.png)

Asking the user to enter the information each time that the program runs is generally better than hard coding the information into the program. At times, however, the user can’t provide the necessary information. Say, for example, that you write a program to send out an invitation to your big promotion bash

![](img/05279073f26be7df99b3c487360dec6a_183_2.png)

to everyone whose name appears in your personal telephone directory — but you don’t want to enter each name individually. So you sit down to write a Linux program to do the work for you.

You follow all the tips that I give you in this chapter and create a subprogram that prints the invitation. Each time this subprogram prints, however, it needs one name from your telephone directory. Of course, you don’t expect the subprogram to prompt you to enter each name. Instead, your program recalls each name from your telephone directory and passes the name as an argument whenever the program calls the subprogram and requests the name variable.

### Passing Arguments

The transfer of the information from the command line to the program (or subprogram) is commonly known as passing arguments. (The information that passes to the program resides outside the program or subprogram that’s using the information.)

Say that you want to run the subprogram that finds a listing in your personal telephone directory. You call this subprogram findlisting and assume that the subprogram doesn’t prompt you to enter the person’s name that you’re trying to locate. Instead, you pass the name of the person as an argument to the program. The following example shows how you enter the information at the command line:

```bash
findlisting Jones
```

The Linux operating system automatically passes the name Jones to the findlisting subprogram. The findlisting subprogram then uses the name to search for Jones’ telephone number. After it finds the number, the findlisting subprogram displays the number on-screen — if the programmer provides the subprogram the necessary instructions to do so.

You start your program by entering its name on the command line, as follows:

```bash
$ displaymenu
```

The $ sign is the command prompt for the bash shell. This prompt already appears on-screen. The name of the program that Linux is calling is displaymenu. You can send data to the program by placing the data to the right of the name of the program, as follows:

```bash
$ displaymenu yes
```

The word yes is the information that you’re sending to the program displaymenu.
