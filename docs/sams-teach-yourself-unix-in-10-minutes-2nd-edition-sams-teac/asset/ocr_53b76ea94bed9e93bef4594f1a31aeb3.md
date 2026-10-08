# LESSON 15

# User Utilities

In this lesson, you will learn how to change settings on your Unix system and modify or alter your environment.

When working with Unix, you will undoubtedly come to a point where some form of customization is required. For instance, we talked about logging in to your Unix system, but what about changing your password? We have also discussed the shell many times, especially in the last lesson on shell scripting, but what if you want to change your shell? These and other methods of customization will be discussed within this chapter.

# Using chsh

In our discussion of shells earlier in this book, we have talked many times about what shell you are using or what shell prompt commands you can perform. We have also touched on why you may want to change your shell, and now we will cover how to just that within your Unix environment.

In the beginning of this book, you learned that there are a variety of different shells that you can run; covered most if not all of them. There will be times when you want to change your shell, and to do that, you can use the change shell command, or chsh. The chsh command will allow you to choose one of the shells that is registered for use on your machine. This means that you must have a shell on your system in order to request it.

One problem you may encounter is not knowing which shell to choose; after all, there are so many shells, and how do you know which ones are registered for use on your system? To solve this problem, you can use the chsh command with the -l option. The chsh -l command will

![](bbox=[0.568, 0.56, 0.893, 0.203])