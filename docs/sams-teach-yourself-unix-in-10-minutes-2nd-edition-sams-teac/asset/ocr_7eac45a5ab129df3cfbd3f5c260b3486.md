# Lesson 4

Each user in a Unix system should have one directory assigned to her for personal use, to store data. This directory is called the home directory.

Your home directory will be where you wind up when you initially log to your Unix system. You will be in your home directory by default.

Anything in or below your home directory belongs to you, and unless you allow otherwise, the contents of this directory will be secure and not available to others for use or browsing.

> What Is Tilde? In Unix, you can refer to your home directory simply as ~. This is important to know because it can reduce the amount of typing you have to do. More specifically, to switch to your home directory, you can want to switch to someone elses home directory, you can also use the tilde with the person's username, see as ~username.

Now that you can the pwd command to find your present location, let's investigate how to view the contents of a directory, whether it be more directories or files.

# Unix File Listing

Up to now, all the commands you have learned have been important. Not one of them is commonly used or seen. This next command we discuss, however will be a command that you use just all the time as a typical Unix user, so we will spend some quality time reviewing its details as closely as possible. The command you do this with is the ls command, which lists files. Issued without any arguments (also known as switches), ls lists the files and subdirectories in the current directory. You can, of course, list files in a different directory by specifying that directory in the path statement or or simply by changing into that directory and then issuing the ls command. An example of using pwd and ls is seen here: