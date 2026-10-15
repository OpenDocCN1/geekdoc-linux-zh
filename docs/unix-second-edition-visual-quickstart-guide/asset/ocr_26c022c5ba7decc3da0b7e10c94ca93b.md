In short, we assume you want to use Unix to achieve your computing goals. You want to know what you can do, get an idea of the potential that a command offers, and learn how to work smart. Very smart.

You can do all of these things using this book. Basically, all you need is access to a Unix account or system and a goal (or goals) that you want to achieve.

# What Do You Need to Know to Get Started?

As you get started learning Unix, keep in mind the following Unix conventions for typing in commands:

+   - Unix terminology and commands are typically arcane, cryptic, and funny-looking. For example, the command to list files or directories is just ls—short and cryptic. We’ll walk you through the commands one step at a time, so you know how to read them and apply them to your own uses. Just follow the steps in the order provided.
+   - Unix is case-sensitive, so type commands following the capitalization used in the book.
+   - Whenever you type a command, you also have to press Enter. For example, if we say: 1. funny-looking command goes here you’ll type in the code, then press Enter, which sends the command along to the Unix system.

+   - Some commands have flags (additional available options) associated with them that give you additional control. For example, you might see the ls command used in variations like ls -lo or ls -l -a. In either case, ls lists the files in a directory. the optional -l flag specifies that you want the long format, and the optional -a flag specifies all files, including hidden ones (don’t worry, we’ll go over this again!). Just keep in mind that flags are essentially options you can use with a given command.
+   - You can also put multiple commands on the same line. All you have to do is separate the commands with a semicolon (;), like this: ls ; pwd which would list the files in the current directory (ls) and find out what directory you’re in (pwd)—all in one step!

So, with these things in mind, see you in Chapter 1!

# Anything Else You Should Know?

Yup! Feel free to contact us at unixvqs@raycomm.com. We welcome your input and suggestions as well as questions related to this book. Thanks, and we look forward to hearing from you!

# Note to Mac Users

For simplicity, we consistently write Enter (not Return), Ctrl (not Control), Alt (not Option), and we refer (not very often, though) to a Recycle Bin (not a Trash Can). No slight intended to those who do not use PCs or Windows—we just tried to keep the complexity of the instructions to a minimum.

```
ls ; pwd
```