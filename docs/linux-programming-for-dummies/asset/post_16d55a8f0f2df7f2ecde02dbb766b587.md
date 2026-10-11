
Next, the computer skips a line on-screen (`echo " "`) and tells the user the kind of data to enter (`echo "Enter Your First Name: "`).

The reserved word `read` instructs your computer to take all the characters that the user enters at the keyboard and place them in the string variable `FirstName`. This command kicks in only after someone presses the Enter key, however.

## Reading a number

If your program needs to read a number from the keyboard, you must take a slightly different approach. The instruction that you give your computer is the same that you give to read a string except that you use a numeric variable. The following code shows you how to tell your computer to read a numeric value from the keyboard.

```bash
#!/bin/bash
clear
echo " "
echo "Enter Your Age: "
read age
```

This code example is the same way that your computer reads a string from the keyboard.

The line `#!/bin/bash` tells the computer to start the bash shell before clearing (`clear`) the screen.

- You don't need to declare the numeric variable at the top of your program.
- The line `echo " "` then tells the computer to skip a line before it asks the user to enter some data (`echo "Enter Your Age: "`).
- You use the reserved word `read` in front of the name of the variable (`age`). Doing so tells your computer to take all the data that the user enters at the keyboard and place it in the string variable `age`.

## Mixing strings and numbers

You can mix the kind of information that your program collects from someone. Sometimes you can ask for a numeric value; other times you can ask for a string value. Your program doesn't care.

> Keep in mind, however, that what you ask for does matter to the person using your program. You must ask for the information in a logical way. Someone using your program doesn't, for example, expect you to ask for a first name, age, and then a last name. That order just doesn't make sense. First name, last name, and age is an order that seems better.

Besides using common sense in requesting information, you also want to ask one question at a time. The following code illustrates how to read both string and numeric data in a logical order:

```bash
#!/bin/bash
clear
echo " * "
echo "Enter Your First Name: "
read FirstName
echo "Enter Your Last Name: "
read LastName
echo "Enter Your Age: "
read age
```

This program does, of course, prompt the user for first name, last name, and then age.

## Displaying Data That Someone Enters

After your program has the information that someone enters, it needs to do something with the information. The program can use the data in a calculation, store the information in a file on your disk, or do practically anything with it that you can imagine. (Well, almost anything.)

The most common thing to do with the information is to make it appear on-screen. Another thing to do is to compare the data with information that's already in your computer — but for now, you want to just try a simple display first.

Following are some things that you need to know about displaying information:

- Data appearing on-screen still remains in the variable. (You store data in a variable, and then the program copies the data from the variable to the screen. The data remains both on-screen and in the variable.)
- This process enables the program to do something else with the data while you're looking at it. Your program can store a salary in the `MySalary` variable, for example, and then display the salary on-screen. While the salary's on-screen, the program can still use it to calculate your new salary — assuming, of course, that you receive a raise in pay.

Data always appears at the cursor on-screen. Say that your program displays the text `Salary:`. The cursor — that flashing little light that signals where you are on-screen — moves to the right of the colon (`:`). Next, your program displays the data that contains the salary.

You can modify data appearing on-screen, but the changed data doesn't automatically appear on-screen. Your program displays the salary on-screen. It also stores the salary in the variable `MySalary`. Your program then proceeds to calculate the new salary and saves the result in the variable `MySalary`. The old salary, however, still remains on-screen until your program displays the variable `MySalary` again.

Nothing's special about the data that your computer collects from the keyboard and stores in a variable. This capability is the same as if your program itself told the computer to assign the value to the variable.

## Displaying a string

A typical Linux program tells someone to enter a string of characters; the program then saves the characters in a variable before displaying them on-screen. You can choose to do either of the following:

- Display the characters on a single line.
- Display a combination of the characters with other characters on a single line.

You can have the computer show just the characters that someone enters into your program by using the `echo "variable name"` on a line in your program. (Of course, replace `variable name` with the name of your variable.)

You can combine characters with other characters by placing them within quotation marks, as shown in the following code. Here, the program asks users their first names and then greets them with a big hello (but no kiss and hug).

```bash
#!/bin/bash
clear
echo ""
echo "Enter Your First Name: "
read firstName
echo "Hello, $firstName"
```

Although the program adds the text `Hello`, you could store this string in another string variable. (I do that in the following example.) By using the following code, you tell the computer to go to the `$Greeting` variable and display that string before going to the `$FirstName` variable and displaying those characters:

```bash
#!/bin/bash
clear
declare FirstName,Greeting
echo $Greeting = "Hello. "
echo ""
echo "Enter Your First Name: "
read FirstName
echo $Greeting $FirstName
```

## Displaying a number

Telling your computer to show a number on-screen isn’t different than telling it to display a string.

![](img/05279073f26be7df99b3c487360dec6a_93_0.png)

Take a look at the following code to see how to show numeric data on-screen. Remember that you don’t need to declare the numeric variable at the top of a program.

```bash
#!/bin/bash
clear
echo ""
echo "Enter Your Age: "
read age
echo $age
```

## Displaying strings and numbers

You collect numeric data and string data separately. Someone who uses your program, however, expects to see them appearing together on the same line. You don’t want to disappoint anyone. So here’s how you can show numeric data combining with string data on the same line:

```bash
#!/bin/bash
clear
echo ""
echo "Enter Your First Name: "
read FirstName
echo "Enter Your Age: "
read age
echo "$FirstName, $age really isn’t that old."
```

The line `echo "Enter Your First Name: "` asks someone to enter a first name and then saves it to a variable (`FirstName`).

Next, `echo "Enter Your Age: "` asks the person to enter an age. It saves this information, too — but to a different variable (`age`).

Finally, the program shows the person's first name, age, and then a comforting comment (that no one believes): `Jim, 82 really isn't that old.`

## Keeping Data in a File

Putting data that someone enters into your file on your hard disk is a common practice. A *file* is like a file drawer (but a lot better organized). Say that you want to keep your date book handy — but away from prying eyes. You can build a program that collects all those special phone numbers for you and then places them in an electronic hideaway on your computer's hard disk. Then, as Friday night rolls around, you can instruct your program to open the file, and you can choose the date of your dreams. (Of course, your dream date may already have plans . . . )

![](img/05279073f26be7df99b3c487360dec6a_94_0.png)

Following are some reasons for saving data to a file:

- Data is always available to your programs.
- You don't lose information unless a disaster happens to your hard disk. And we all know that can *never* happen. (On the other hand, where's my tape backup?)
- You can use a Linux utility to search the file for particular information.

The way in which you organize the data that you save to a file is important; otherwise, your computer may have a difficult time finding it.

In Chapter 16, you explore how to create a simple database. A database is a special kind of file for holding information that you need to find fast. For now, however, I want to show you how to take the data that your program collects and stuff it into a simple file on your hard disk.

### Saving data to a new file

Linus Torvalds decided that any time your program needs to display anything by using the `echo` reserved word, it uses the screen.

That's just fine for most of your programs, but you can easily change your program to display data someplace else — such as to a file. Such a process is known as *redirection*, which means changing the direction of the normal flow of data.
