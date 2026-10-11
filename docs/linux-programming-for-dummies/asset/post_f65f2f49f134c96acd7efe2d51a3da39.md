
# 6 Where to Go from Here

Now’s the time to launch your exploration into the world of Linux programming. Grab a comfortable chair, sit back, and get ready to have some fun.

# Part 1: A Beginner’s Introduction to Linux Programming

![](img/05279073f26be7df99b3c487360dec6a_30_0.png)

## In this part . . .

If you think that the great-paying jobs go to computer programmers and you're not one because computer programming seems too complicated, this book is for you.

You hear about computer programming at work or on television, and you hear that the kids in your old high school know how to do it. You'd like to give it a try, but you don't know where to begin.

Guess what? You already started as you opened this book. You don't find pages of technical computer jargon here. You do find the first steps that you need to begin programming a computer.

# Chapter 1: Checking Out How Linux Programming Works

## In This Chapter

- Understanding the Linux programming development cycle
- Writing, naming, and running a Linux program
- How Linux shell-script languages differ from other languages

The primary reason for writing a computer program is to make a computer do something useful. To begin writing a Linux program, you first want to turn off your computer and then use some paper and a pencil to plan exactly what you want to make the computer do.

You can make a computer do virtually anything that you can imagine, short of making it take your driver's test or using it to print money to pay your bills (although some people do use computers illegally to print money). A computer program can perform such basic tasks as displaying a few words on-screen or more complicated tasks, such as tracking an airplane flight across the country.

After you determine what you want the computer to do, you must write down step-by-step instructions in a programming language to tell the computer how to do what you want.

## Writing a Linux Program

Just as millions of ways exist to earn money, millions of ways also exist to write a computer program correctly. Some people work with their hands to make buildings; others draw up construction plans; and some folks spend their time trying to figure out how to marry into a wealthy family. Similarly, you can write the same computer program in an unlimited number of ways; no matter which way you write it, however, the result is always the same—a *program*.

Your job is that of *a programmer*, or the person who writes a computer program. You want to write programs that are easy to use, of course, and that correctly tell a computer what to do. No one can use a program that doesn't work correctly (although that doesn't stop you from selling your programs before you're run out of town), and a program that's difficult to use frustrates anyone who uses it—and people often toss it in the garbage, even if it works fine.

To make sure that each program you write gets the job done, you need to test it to make sure that you're on target. If you design a program to display names and addresses on-screen but it prints names and addresses instead, the program obviously doesn't work (unless, of course, you change the program's intent to printing names and addresses).

Deciding whether your program is easy to use, however, is a difficult job. What you may think is easy can prove an insurmountable task for someone else. Everyone *knows*, for example, how to board a bus, pay the fare, find a seat, and get off the bus at the right bus stop, even if she's never traveled on that particular bus line. The same concept applies whenever someone uses your Linux program (if you make it easy to use, of course). Users expect to start your program by typing the name of the program into the computer or choosing your program from a menu that appears on-screen. After your program is running, users expect menus that walk them through each step and screens that demonstrate a logical flow. The structure of your program should be similar to other programs and familiar to anyone who uses it.

## Understanding the Linux Programming Development Cycle

The following nine steps are necessary to create a Linux program (the same number of innings necessary for a no-hitter in baseball—unless it's a rain-shortened game), with the first eight steps being the *development cycle*:

1. Decide what you want the computer to do.
2. Decide how your program is to look on-screen (the *user interface*).
3. Create the user interface by using common objects such as text and areas in which users can enter information.
4. Arrange these common objects into a logical flow on one or more screens.
5. Write instructions in Linux to make each part of the program do something.
6. Run the program to see whether it works.
7. If your program doesn't work, say out loud, "I hate computers!" (and then remember that computers do only what you tell them to do).
8. Look for errors (known as bugs) in your program.
9. Start over (not optional).

Don't plan to memorize these nine steps. Plan to follow them, however, every time that you write a computer program. No shortcuts are available, and you can't skip any steps. Skipping a step is similar to trying to run before you get out of bed, get dressed, and jump out on the sidewalk: You can move your legs as fast as they can move, but you don't get anywhere. (If you tire of this fruitless effort, you can always just stop, roll over, and pull the covers over your head.)

Guess which step is the most difficult? The first step! After you know what you want a computer to do, you must find a way to give the computer the correct instructions. The trick to completing this step is to lock yourself in a room with plenty of junk food and caffeine sources and keep plugging away until you succeed.

## Developing the User Interface

A user interface is simply the method that you use for giving commands to a computer as a program's running, enabling the computer to respond. This interface is what a program displays on-screen and includes which keyboard keys users must press to use the program.

The user interface in a Linux program doesn't feature the exploding screen or rainbow-colored windows that you see in Microsoft Windows programs. Your creativity alone must create excitement from the sparse screens that you can build in Linux.

But don't use this limitation as a crutch! You still can create easy-to-use Linux programs, even if you can't use all the bells and whistles that a Windows program can offer.

## A Quick (and Incomplete) History of Linux

Before you begin to write Linux programs, you may find the story of Linux programming’s origins of interest.

Back in 1991, Linus Torvalds was a University of Helsinki undergraduate student who wanted to run the Unix operating system on his PC. Unix cost more than what Torvalds could afford, so he got together with fellow student programmers, and they created their own version of Unix, naming it Linux. (*Lin* comes from *Linus* and *ux* from *Unix*.)

Three years passed before the first version of Linux was introduced to the public. About 125,000 people were the first to use Linux. The number of Linux users stands at about 10 million today. Version 2.2 of Linux enjoyed the following key advantages over its chief rival DOS:

- Linux uses *demand-page virtual memory*, which is a fancy way of saying that Linux stores the portion of a program that it doesn’t use on disk if insufficient space remains to store the program in memory. This feature enables you to run large programs.
- Linux is *multitasking* and can run more than one program at the same time.
- Linux *works with more than one user* at a time, which is perfect for network servers that require more than one person to access the server at the same time.
- Linux is *free!*

Before Linux came Unix. Back in the 1960s, some Bell Labs employees set out to build a program that enabled a computer to become a *multitasking operating system*, an operating system that runs more than one program at the same time. They used the same clever program to enable more than one person to use the same computer at the same time, which is known as a *multiuser operating system*.

The name given to this brilliant program was Unix. Unix is more than one program; however, it’s a group of programs divided into the following three parts:

- *Kernel*: Controls the parts of the computer, such as the hard disk, memory, and other stuff that makes the computer work.
- *File system*: Makes sure that you don’t lose your information.
- *Shell*: Controls how the computer works.

The Bell Labs folks also tried to make controlling a computer easy. They built many programs into Unix, each of which does something well. These programs, known as *utilities*, can sort information, search for information in a file, and perform a variety of other tasks. You can find out more about utilities in the section “Linux utilities already exist,” later in this chapter.

Those computer whiz kids came up with a way to make using a program much easier than ever. Now programmers can combine just the utilities you need into a Unix program called a *shell script*. This script enables you to write complex, sophisticated Unix programs in just a short time. All the tricky stuff is already programmed into the utilities. You just need to choose the right ones and combine them into the programs that you write.

By the 1980s, these Unix features, in addition to the rapid creation of powerful and low-cost computers, brought Unix from the halls of universities and the Department of Defense (DoD) into industry.

Today all the development that went into the creation of Unix is carried over to the version of Linux that you’re using to write and run your programs.
