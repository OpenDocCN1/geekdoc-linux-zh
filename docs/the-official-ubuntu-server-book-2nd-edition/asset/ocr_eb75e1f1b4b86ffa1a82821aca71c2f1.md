AFTER YOU HAVE COMPLETED AN Ubuntu server install, you might think to yourself, “Now what?” If you are new to Linux administration, you might feel a bit overwhelmed at the steep learning curve you see. For one thing, there are a large number of command-line tools to learn. For another, there are all sorts of configuration files scattered in different locations. Even if you are an experienced Linux administrator but new to Ubuntu, you will find that configuration files might not be quite where you expect, and some programs you are used to might not even exist. In many ways trying a new distribution is like driving a new car. Sure, the car has a steering wheel, a gas pedal, and a brake, but it still takes you a minute to adjust the mirrors, find out where all the gauges and controls are, and adjust the seat until you feel comfortable. Think of this chapter as that minute or two behind the wheel of a new car. Here I cover some core commands a new administrator should know, explain the Ubuntu boot process, describe the main directories that make up an Ubuntu system, and talk a bit about networking. By the end of the chapter you should feel pretty much at home while logged in to your Ubuntu server.

# Basic Command-Line Administration

Entire books have been written on command-line tools and how to use them effectively, so instead of documenting every major Linux command and process, I’m going to assume you are new to Linux server administration and need at least a basic set of tools just to move around the system, edit files, and check processes. If you are an experienced administrator, feel free to skip ahead to the next section where I document the Ubuntu boot process.

# Move Around the System

When you log in to your server, the first thing you see is a blinking cursor. By default, when you log in you will be in your user’s home directory. If you want to confirm this, you can use the pwd command:

```
```bash
$ pwd
/home/kyle
```
```

One of the most common commands an administrator runs is the ls command. If you come from a Windows background, this is a lot like the dir