
boot-process process until it gets to the login prompt. Instead of the text-based login screen, however, the X Window System environment launches. From this environment, the graphical enviorment or shell in which you will work is loaded. The most common graphical environment is KDE, although GNOME is also common; both are covered later in this chapter. To log in to Unix graphically, you will be presented with the same credential request, instead of seeing it in the command line, you will see it in a dialog box. After you supply the correct credentials, you will be logged in the system, and you can continue your work or lessons.

Consider a graphical login. Instead of sitting down at your Unix terminal, you may be sitting in front of your home PC with Linux installed. You boot up your system and are presented with a dialog box with the basic information such as needing your credentials (username and password), but you may have other options available to you as well, such as the ability to change the session type. In any case, other than for the presence of a few commands that you can graphically and manipulate with your mouse, text-based and graphical logins are still requesting the most basic of information, which is your username and password.

> **Keyboard Shortcuts**: When using Unix, you should get used to some new keyboard shortcuts because you will be working within the command line and more. Knowing a few shortcuts can save you a lot of time navigating the shell. Use the Tab key within the GUI to shift fields. For instance, after you type in your username, use the Tab key to get to the next field. This will allow your hands to remain on the keyboard and not have to reach for the mouse. This is one example of how you can save time while navigating not only Unix, but also the keyboard.

## The Logout Process

You have completed working in your Unix session and now want to log out. Whether graphically or text-based, you should consider a few things before you do. Logging out is also a fairly simple process. There are a few important things to consider when logging out. First, before logging out, always remember that Unix is a multiuser platform that could be serving hundreds of clients at one time. Make sure that you consider these users as well. When you log in, you identify yourself to the system. Therefore, Unix knows about any files you open. Unix knows when you decide to log out; if you forget something such as a program you have left running during the logout process, Unix will close it for you because it has tracked your activity. This is one example of the power of Unix.

Another concern is security. To remain logged in to Unix all the time is also a security risk. You should always remember to log out whenever you are done with a session. Here is one example of forgetting to log out can hurt you. Imagine being at work and logging in to a system in the morning and leaving at the end of the day and forgetting to log out. Consider that someone else could wander along and now change things in the system “as you,” because he or she would be logged in with your credentials. Remember that credentials are your username and password, which usually tie to an account on the system with your personal information associated with it. Now, things were changed, you don't know what was changed, even if you say it wasn't, it was your account. This could lead to significant problems, so better to be safe than sorry. In short, learn to log out and understand the importance of it.

Logging out of a Unix system is fairly easy. Let's take a look at how to do it using both text-based and graphical methods.

## Text-Based Logout

When working within the shell prompt, all you need to do to log out is type “logout.” The command would be seen as

```bash
> logout
```

Once you issue the logout command, the Unix system will immediately return to a login prompt. You have just successfully logged in and out of a Unix system. If it was your first time, you should be proud of yourself—this was quite an accomplishment. If you have done this once or twice before, continue to practice, because practice makes perfect and this is one task you will master in no time. Remember, you must log in to a Unix system to work within it. Also remember that even though this may have been a somewhat easy task, there were many things to consider, mainly your environment, your security, and your data integrity. One last thing to mention about logging out would be to consider the many different distributions of Unix available today. Some distros may not accept the logout command. Some expect other commands such as exit. A common error message of “Not login shell” may indicate the need for the exit command.

## Graphical Logout

When logging out of your Unix system graphically, you will need to take more steps than when logging out using the text-based method. When logging out of a text-based session, you simply need to issue the command. Within a graphical environment, you need to manipulate the graphical environment to log out. The icon you see that indicates the main menu in which the logout process is initiated may vary depending on your Unix distribution, but in most cases, the first icon (sometimes represented as a K or the SuSE logo), produces the Logout... command from menu. Once selected, you will be given an option to end your session, turn off your computer, restart your computer (warm start), or simply cancel your logout and go back to your current session.

> **With No Mouse**: Don’t forget your keyboard shortcuts as the Tab key. Remember that not all systems come with a mouse, but all require a keyboard. This is determined by systems BIOS startup. You will always have a keyboard to work from, so you should really consider logging in and out of your Unix system without the use of your mouse as much as possible. It’s not common to find mice on Unix systems.

## Shell Game

You are now the master of logging in and out of Unix. If you are not a master yet, continue to practice until you are; each lesson after this builds in complexity, so this skill must be mastered. As we mentioned previously, the true power of Unix is within the text-based environment, where you can execute every command. Again, the only problem with this is knowing how to manipulate these commands.

## Getting Started

Experienced Windows users will know that Windows, when conceptualized, was intended to run on top of DOS (disk operating system). Windows installed on top of DOS to make a complete operating system. Windows was the environment, and there were a few different versions of DOS available. Now, apply the same concept to Unix. The shell (the prompt you just worked to log in and out) can also be changed. You applied KDE to get your environment. The concepts behind all shells are the same, now that you understand what a shell is, let's go over the different types available and most commonly used.

![](img/9552a570ce35faac09a770fd5ff1ede3_29_0.png)

> **This Shell Smells a Bit Fish**: One of your goals Unix should be to not let any of the lingo scare you. A shell is nothing more than a preference. Most commands and functionalities are the same between shells. Unless you are a hardcore developer and well versed in Unix, most times, you will use and continue to whatever environment you grow accustomed to learning. However, one great thing about Unix is the fact that you can change your shell easily once you know how. This adds a deep layer of flexibility into an already powerful engine.

As we mentioned, Unix has a wide variety of shells that you can choose from, and many of the major differences between them are related to programming with them. Programming is usually based around the need to automate a process or job. With this in mind, remember that the shell changes the way you program. You can write a shell script. A script is nothing more than a file that calls commands to automate a process. We will learn more about shell scripting in Lesson 14, “Shell Scripting Fundamentals.”
