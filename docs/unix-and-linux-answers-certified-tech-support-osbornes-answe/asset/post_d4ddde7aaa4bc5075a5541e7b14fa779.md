
group and you need to quickly move to the project’s working directory—`/users/shared/projects/newmodel/colormatch`. That’s a real handful, and not something you want to type every time! So try this:

```
PHOME=/users/shared/projects/newmodel/colormatch
export PHOME
alias goproj=cd $PHOME
```

Include this in your **.kshrc** file, and it will be available whenever you need it. The best part is, if you change to a different project, all you do is change the variable. Your fingers get to continue to use the same command.

## Is there a command I can use to return quickly to my home directory?

Yes; try `cd` all by itself. This little trick will get you back to your home directory quickly, no matter how far away you have managed to stray.

## Can I use ~ as a shortcut to my home directory?

Yes. When you want to describe a directory or file that can be found below your home directory, save yourself some typing by using `~` as a shorthand for your home directory. For example, to get to your personal **bin** directory from anywhere, type `cd ~/bin`.

## Can I use ~ as a shortcut to someone else’s home directory?

Yes. When you want to describe a directory or file that can be found below someone else’s home directory, save yourself some typing and figuring out exactly where their home directory is by using `~` plus their user name as a shortcut to their home directory. For example, if you know that Gladys Meep has a useful set of utilities stashed in her home **bin** directory, you could get to it, assuming she has her permissions set to allow this, by typing `cd ~gmeep/bin`.

## Can I define a variable to describe any directory or filename I use a lot?

Yes! Shorten the long path name to any file or directory you use a lot simply by substituting the variable in the command. Make sure you remember to **export**—or setenv in csh—the variable, however, and include it in your **.kshrc** or **.cshrc** file. This way, it'll always be available.

## Chapter 4

## vi

## Answer Topics!

- **THE MANY MODES OF VI** 44
  - Working with a modal editor and the modes of vi
  - Moving between modes in vi
  - Moving between ex and vi

- **THE BASICS OF USING VI** 45
  - The versions of vi
  - Editing a series of files using vi
  - Editing and saving changes to one file and moving to the next
  - Backing up and editing the previous file in the file list
  - Reloading the current file
  - How to pronounce “!”
  - Viewing files left to edit
  - Starting over on the same list of files

- **MOVING AROUND** 47
  - The basic cursor movement keys in vi
  - Paging through a document one screen at a time
  - Moving the cursor a half page at a time
  - Moving to the top or bottom of a file
  - Moving to the beginning or end of the current line
  - Re-setting the screen
  - Other movement commands in vi
  - Using the “cursor” keys in vi
  - Viewing where you are in the current file
  - Swapping two characters
  - Changing the case of a character you’ve typed

- **INSERTING AND REPLACING TEXT** 50
  - The basic text insertion commands in vi
  - Retyping a word you’ve just entered
  - Restarting text insertion
  - Undoing changes to the current line
  - Replacing the current character and inserting text without overwriting
  - Replacing the entire current line
  - Using the c command
  - Repeating the last text change

- **SEARCHING FOR (AND REPLACING) TEXT** 53
  - Finding text
  - Searching for and replacing text
  - Running substitute
  - Executing a command on an entire file

- **CUTTING AND PASTING** 56
  - Cutting a line into the paste buffer
  - Copying a line into the paste buffer
  - Cutting a character into the paste buffer
  - Using the dd command versus yanking
  - Using named buffers for easier editing
  - Using named buffers for a paste operation
  - Putting the contents of the paste buffer after the current line
  - Cutting a word into the buffer
  - Changing the look and feel of the editor

- **MACROS** 61
  - What macros are
  - Automating frequently used sequences that start in command mode
  - Automating frequent tasks that start in text insertion mode
  - Creating a text insertion mode command to see where you are in the current file
  - Reducing the number of keystrokes needed to enter common phrases

- **OTHER ESSENTIAL COMMANDS** 64
  - Saving changes and quitting vi
  - Including another file in the current file
  - Writing out part of the current file to a "scratch" file
  - Quitting without saving
  - The "smart" exit command
  - Getting a word count or line count
  - The other editor—emacs
  - Recovering a file

## vi @ a Glance

Whatever your interaction with UNIX, sooner or later you’ll need to edit a text file. And then you’re faced with that most wonderful of text editors—vi. Before you start using vi, however, it’s best if you understand its modes, for it works quite differently than the text editors you’re probably used to.

Once you’ve learned **the basics of using vi**, you’ll be able to open a file or files for editing, and manipulate these files as you wish.

The vi commands for **moving around** within a file are not difficult to learn, but they’re not exactly intuitive either. In order to work efficiently, it’s helpful to know the quickest way to get where you want to go.

**Inserting and replacing text** are the two most basic functions of any text editor. Whether you want to change a character, word, or entire line, here are the commands that will make vi do your bidding.
