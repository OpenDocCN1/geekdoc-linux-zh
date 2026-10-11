
The purpose of this program is to display a simple menu on-screen. For this example, you’re going to make a telephone book menu that looks as follows as your program runs:

```
The Telephone Book
1. Display A Telephone Number
2. Add A New Telephone Number
Q Quit
Enter your selection:
```

Follow these steps to create your program:

1. Type `vi mymenu` at the command prompt.
   - This command starts vi and names your program *mymenu*.
2. Type `i` after the *blank (except for the titles) page appears on-screen*.
   - This command takes you to the insert mode.
   - If you choose to use another text editor besides `vi`, you don’t start the text editor by using the commands shown here. You probably can find how to use the text editor by typing `man text editor name` at the command prompt. (Of course, use the name of your text editor instead of typing *text editor name*. If you’re using `emacs`, for example, you type `man emacs`.) The manual pages for your text editor should then appear on-screen. If they don’t, the manual pages aren’t on your computer. Call the person who’s responsible for your computer and ask that he install these pages.
3. Type the Linux code that follows on the *blank page*:

```bash
#!/bin/bash
clear
echo " "
echo "The Telephone Book "
echo " "
echo "1. Display A Telephone Number "
echo "2. Add A New Telephone Number "
echo "Q.Quits"
echo ""
echo "Enter your selection: "
```

Here’s what you’re doing!

You’re starting the *bash* shell script by using `#!/bin/bash` as the first command of your program.

Next, you're using the clear reserved word to tell your computer to erase any text that may already appear on-screen.

You're then using the echo reserved word to display text as well as blank lines on-screen. All the characters between the quotation marks appear on-screen.

Of course, you don't need to copy this program exactly. Become a little adventurous and experiment. Change the text, change the spacing — go a little crazy. This kind of experimentation is the only way that you really discover how to create a Linux program.

## Saving your program

After you're satisfied that all the instructions in your program are in the correct order and that you're using the correct words to tell the computer what to do, you're ready to save your file.

Following are several ways to save your file by using the vi text editor (some of which are familiar to you if you first read the section "Stopping vi and saving changes," earlier in this chapter):

- **ZZ**: Saves your file and exits vi.
- **:w**: Saves your file without exiting vi.
- **:wq**: Saves your file and exits vi.
- **:w filename**: Saves your file under a new name that you specify (so that :w mymenu2: for example, saves your file as mymenu2).

Always save your program while you're still writing your program in vi. Until you save your program in a file, everything that you type exists only in your computer's memory. If you turn off your computer (or the power company does it for you), you lose all your hard work!

## Making your program work

Your program is almost ready to run . . . but not just yet. You still must tell your computer that your file is an executable file. An executable file is a file that contains instructions for your computer to follow.

Follow these steps to tell your computer that your file is executable:

1. Move to the directory that contains your file if you're not already in that directory by typing the following command at the prompt:

   ```bash
   cd /mydirectory
   ```

   Remember to replace mydirectory with the directory name on your computer that contains your program file.

2. Make the file an executable file by using the chmod utility, typing the following at the command prompt:

   ```bash
   chmod 711 mymenu
   ```

   This command enables everyone to run your mymenu program — but only you can see the file itself. (Refer to Chapter 1, where I explain a little about the chmod utility.)

3. You can run your program by typing the name of the program at the command line as follows and then pressing Enter:

   ```bash
   mymenu
   ```

   If you have problems running your mymenu program, try running the program as . /mymenu.

   The program displays the menu on-screen and prompts you to enter a selection from the menu. After you enter your selection, the program ends.

## Making changes to your program

You can change your program at any time by recalling your program to the screen by using the vi text editor or the text editor of your choice.

Using vi as my model, for example, I simply type vi mymenu at the command prompt. Here I can start vi again and use the name of the program file. Remember that, after you first start vi, you're in the command mode.

Expect to edit your programs frequently. Always make another copy of your program under a different name before you begin changing your program. You can use this backup copy of your program in case you accidentally destroy your program during editing.

# Part II

# The Basics of Writing Code

![](img/05279073f26be7df99b3c487360dec6a_76_0.png)

# In this part...

Great! You’ve reached the point where you actually start writing Linux code to make your computer do something worthwhile. So far, you’ve discovered the finer points of building a user interface (with an occasional Linux command sprinkled here and there).

What matters to those who use your program is what your program can do for them. Just because you design the perfect plan for your program doesn’t mean that your work is done.

Writing instructions for a computer can intimidate even the hearty adventurer, but you have nothing to fear. Writing Linux code is as simple as giving someone step-by-step instructions: You’ve done that most of your life.

*Caution: Programming is addictive and a whole lot of fun after you get started. So don’t waste any more time: Start to code.*

# Chapter 4

# Getting Indecisive with Variables

## In This Chapter

- Understanding data
- Understanding variables and values
- Assigning numbers and strings to variables
- Declaring data types
- Making a string array

After you know what you want your computer to do, the time is right to write Linux code. The place where you begin to write your Linux code is in a text editor file (as I explain in Chapter 3).

Your text editor file that contains your program just tells your computer to do something. The simplest program that you can write tells your computer to stop running your program. You use only the reserved word exit in this program, as shown here:

```bash
exit
```

You want your programs to do more, however, than just this task. You can, for example, design a program to ask someone for a name and address. You also need to write instructions into your program to tell the computer to read this information and do something with it.

In this chapter, I tell you all about how to store and use information in your program: You create a storage space inside your computer's memory and then place your information into that space. Of course, I also tell you how to retrieve the information for use by your program.

Information that your program receives from someone who uses it is known as **data** — now you also know where the character on *Star Trek: The Next Generation* got his name. Good programs follow these three simple steps:

1. They get data from the keyboard or a file.
2. They do something with the data.
3. They show the data on-screen or in a report.

The reason for writing your program is to turn your computer into an electronic factory. In one end goes all the data that the computer needs to do something. And out the other end comes useful information. This information processing is all that a word processor, a spreadsheet, and a database program actually do. And the data that all these programs use manipulates only two things: *strings* and *numbers*, as the following sections describe.

## Strings

A *string* is usually a bunch of letters or characters that you… well, *string* together. A character can be a hyphen or any character that you find on the keyboard. A string can consist of just a *single* letter or character, too. An entire sentence can also be a string. And this entire chapter can be a string as well. In fact, any group of letters, spaces — and even numbers — can act as a string (as you see in the section “Variables 101,” later in this chapter).

## Numbers

A *number* can consist of any type of number, such as amounts of money, someone’s age or height, the number of friends who come over to your cookbook (and don’t invite you to their cookouts), and so on. This category includes positive and negative numbers as well as whole and fractional numbers.

And, to complicate matters, numbers are also characters! This dual-identity situation may seem a little confusing to you, at least at first, but it isn’t so confusing to your computer. If you tell the computer that the number is part of an address or telephone number, the computer treats the number as a letter or character. If you tell the computer to add (or perform any mathematical operation) using numbers, however, the computer treats these numbers as numbers (and not as characters). Clear? Well, keep reading.
