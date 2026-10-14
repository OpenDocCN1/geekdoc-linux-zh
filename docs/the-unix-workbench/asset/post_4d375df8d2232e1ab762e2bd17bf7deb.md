
```
cd Music
```

As you can see the path to the current working directory has changed:

```
pwd
```

```
## /Users/sean/Music
```

I specified a **relative** path when I entered cd Music. The path to the Music directory is just Music/ relative to my previous working directory. I can go back to /Users/sean/ with the command cd .. which changes the working directory to the folder above the current working directory:

```
cd ..
```

```
pwd
```

```
## /Users/sean
```

Notice that .. is also a relative path, since it specifies the directory above your current working directory. Similarly . is the path to your current working directory. Therefore since my current working directory is /Users/sean then cd Music is the same as cd ./Music.

I can cd to any folder as long as I know the **absolute** path to that folder. For example I can cd to /Users/sean/Music by entering the following into the shell:

cd ~/Music
pwd

```
## /Users/sean/Music
```

It doesn’t matter what directory I’m in since I’m using an absolute path, I can jump straight to that directory (Remember that ~ is a shortcut for the path to your home folder). Of course you shouldn’t expect yourself to have every absolute path on your computer memorized! You can use a terminal feature called **tab completion** in order to speed up typing paths and other commands. Enter the following into your shell, and then try pressing the Tab key (on some machines you need to press it twice):

```
cd ~/
```

(press Tab)

```
## Desktop
## Documents
## Photos
## Music
## todo.txt
```

Pressing tab shows you a list of all files and folders inside of the ~/ directory. Now I’m going to type ~/D into my terminal and you can see what happens when I press tab again:

```
cd ~/D
```

(press Tab)

```
## Desktop
## Documents
```

Since I added a "D" to the path, only folders with names that start with a "D" are listed. If I type cd ~/De into the console and then press Tab then the command will autocomplete to cd ~/Desktop/. If I press tab again, the console will list all of the files and folders on my desktop.

Make sure to pause and try this yourself in your own terminal! You won’t have the same files or folders that I do, but you should try using cd and tab completion with directories and files that start with the same letters.

# Summary

- You can identify a specific file or folder by its path.
- The root directory (/) contains all of the folders and files on your computer.
- Your home directory (~) is the directory where your terminal always starts.
- Use the cd command to change your working directory.
- The pwd command will print the working directory.
- The ls command will list files and folders in a directory.

# Exercises

- 1. Set your working directory to the root directory.
- 2. Set your working directory to your home directory using three different commands.
- 3. Find a folder on your computer using your file and folder browser, and then set your working directory to that folder using the terminal.
- 4. List all of the files and folders in the directory you navigated to in #3.

# Creation and Inspection

Now that you can fluidly use your terminal to bound between directories all over your computer I’ll show you some actions you can perform on folders and files. One of the first actions you’ll probably want to take when opening up a fresh terminal is to create a new folder or file. You can make a directory with the `mkdir` command, followed by the path to the new directory. First let’s look at the contents of my home directory:

```
cd
ls
```

```
## Desktop
## Documents
## Photos
## Music
## todo.txt
```

I want to create a new directory to store some code files I'm going to write later, so I'll use mkdir to create a new directory called Code:

```
mkdir Code
ls
```

- ## Desktop
- ## Documents
- ## Photos
- ## Music
- ## todo.txt
- ## Code

It worked! Notice that the argument Code to mkdir is a relative path, however I could have specified an absolute path. In general you should expect Unix tools that take paths as arguments to accept both relative and absolute paths.

There are a few different ways to create a new file on the command line. The most simple way to create a blank file is to use the touch command, followed by the path to the file you want to create. In this example I'm going to create a new journal entry using touch:

```
touch journal-2017-01-24.txt
ls
```
