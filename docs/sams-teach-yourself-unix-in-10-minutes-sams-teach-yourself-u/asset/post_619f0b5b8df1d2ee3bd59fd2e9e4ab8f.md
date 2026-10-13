
Your script will, if everything works, produce exactly the results which were outlined at the beginning of this section.

To explain a few of the things that happened in this shell script, the following might be helpful—most of this will be understandable from what you've learned thus far:

- **echo**—This command puts things on its STDOUT. Here it is used to create a STDOUT stream containing "Howdy Neighbor," which is then fed to the mail STDIN via a pipe.
- **mail**—This command can take a message on STDIN and send it to a list of recipients. (mail is discussed in Lesson 18, "Accessing the Network Resources.")
- **grep**—You know what grep does, and what tail does. After the last 100 lines matching bob have been found, they're handed to lpr on its STDIN. lpr sends data to a printer. (lpr is discussed in Lesson 17, "Printing.")
- **xterm**—Starts a terminal, and can be told to start a program running in the terminal window by using the -e option.

## So Many Shells on the Beach

As has probably become apparent to you if you've spent as much time playing with your UNIX account as you have reading this book, UNIX has an abundance of shells available for you to use. The syntax and available commands in each of these shells ranges from subtly different to extremely different. For the purposes of this lesson, you'll be using commands and syntax compatible with csh and tcsh.

The bourne shell, sh is probably the best shell to write scripts in if you're concerned about distributing large sophisticated scripts to unknown users. It's not the easiest shell to use at the command line, though, so you're better off starting with the same shell you use in day-to-day life.

## DOING IT AGAIN AND AGAIN: foreach

Instead of spending time collecting commands into a file to automate them, you can get a lot of mileage out of simple automation techniques that don’t involve putting commands in files at all. One of the commands used for this is the foreach command.

## EXECUTING A COMMAND OVER AND OVER

If you find yourself in a situation where you need to repeatedly execute some action for each file in a set of files, the foreach command can help. It takes a list of files, and does something "for each" of them. The use is much easier to demonstrate than to explain. If you have a list of files that you need to do something to, you can follow these steps to use foreach:

- 1. Figure out what you want to do. In this example, you’ve got a bunch of directories, and you want to create a tarfile of each.
- 2. Decide on the names of the files/directories that you want to do your something to. In this case, you’re going create tarfiles for the directories mydirectory, yourdirectory, and herdirdirectory.
- 3. Pick a variable name that you want to use; here you’re just going to use a variable named test. It doesn’t much matter what the variable name is, just so long as it doesn’t conflict with the name of the command.
- 4. Issue the foreach command as foreach <variablename> (<filenames>). The foreach command then asks you what you want to do for each file by displaying a question mark. Fill this in with whatever you need to do. Again, you’re going to be tarring files in the example. After giving foreach the command for whatever it is you want to do, finish it by putting the command end on a line by itself.

To illustrate the example, type the following:

```
> foreach test (mydirectory yourdirectory herdirdirectory)
? tar -cvf $test.tar $test
? end
```

Your machine will respond by running the tar command for each file you gave it to work with. Inside the foreach command loop, note the use of the expression $test. foreach goes through the list of filenames you gave it and puts each one sequentially in the test variable. To use the contents of a variable in the shell, put a $ sign before it. For example, foreach first puts mydirectory in the variable test. It then runs the tar command, and the shell expands the test variable to mydirectory. The tar command that gets executed actually looks like the following: tar -cvf mydirectory.tar mydirectory. The next time through the loop, foreach puts yourdirectory in the variable test, and the process is repeated.

You can use regular expressions in the shell instead of enumerating the filenames to use the foreach command. If you notice in the previous example, all the directories you want to tar actually have part of their names in common—directory, in this instance. If you wanted to produce the same results without having to enumerate all the directory names to foreach, you might issue the preceding foreach command as follows: foreach test (*directory) You can use the pattern matching tools you learned about in Lesson 13, “Regular Expressions,” to match any collection of filenames you want.

## RENAMING MULTIPLE FILES

You’ve probably noticed that the mv command can’t do some really convenient things, such as renaming multiple files with new names instead of new locations; this is an ideal problem for foreach.

For example, imagine you have a bunch of files for a pet project, and they’re named things such as brokenjunk.start, brokenjunk.today, brokenjunk.gif, and so on. Suddenly your boss decides that it’s important that you give these files to the development department because they want to demo your project next week. This never happens to you, right? If it did, you might want to rename your files to something a little more professional. Instead of renaming the files one by one, you can use the foreach command to automate the task for you. In this case you might type the following:

```
> foreach test (brokenjunk.*)
> mv $test importantstuff.$test:e
> end
```

The part of this you might not immediately understand is the $test:e part. This says, “Expand the $test variable and toss out everything except for the stuff after the last . in the filename”—in this case, the parts that make the files different (start, today, and so on).

Of course, this isn't a very useful command for three files, but if you've got a project with hundreds of files it can save you a lot of typing.

## Modifying and Replacing Originals

Another useful trick for which you can use the foreach command is when you need to apply a process to each of many files—and you want to do it without creating new files, instead just replacing the old ones in-place.

Say you have a collection of image files, each of which have a border which you want to crop off, and then you want to scale them to a smaller size. If the imaginary command crop took files on STDIN and wrote its data to STDOUT, you might use the foreach command similar to the following:

```
> foreach test (*.gif)
? crop < $test > holding
? mv holding $test
? end
```

Why not just do crop < $test > $test? Because you can't be guaranteed to get away with writing to the file while you're still reading from it—so you store the results in a temporary file named holding. Follow up by using the mv command to move the temporary file back to the original filename.

## Doing it After a While: sleep

The utility of a command that just sits there for a while is perhaps not readily apparent, but you will find uses when you have actions you want to repeat at relatively short intervals. If you do run across a situation where you need a shell script to pause for a while, you can use the sleep command. Simply issue the sleep command as follows: sleep <seconds>. The shell halts until that many seconds have passed. It then resumes execution of whatever it was doing.

## DOING IT CONDITIONALLY: while AND if

If you want to get sophisticated with the control of your automation, you can turn to conditional statements that can activate certain sections of your script only when certain conditions apply.

To use conditional statements, you need to create a condition for the statement to test. This can be as complicated as you want, but for now, you need to stick to simple things such as equal to.

## while

The while command, with the syntax while <condition>, does things while a certain condition holds.

Although the following example is amusing, consider the situation where you're feeling really lonely and want to get some email. When you execute /bin/mail, all it tells you is No mail. A sad day indeed. So, to try to brighten your day, you've written yourself a little script that sends email to a few of your friends every so often, asking them to email you back. Of course you don't want to be such a bozo that it keeps sending them email even after they've replied, so you want it to stop after you've received email, or to only continue while you don't.

If you actually wanted to try this, you might accomplish it by entering a little script such as the following:

```
> set hopeful=`/bin/mail | grep -cv No`
> while ($hopeful==0)
> echo "please send me mail" | mail myfriend@somewhere.com
> echo "please send me mail" | mail anotherfriend@elsewhere.com
> sleep 60
> set hopeful=`/bin/mail | grep -cv No`
> end
```

This silly little script is making use of grep to count the lines (-c option) which do not (-v option) contain a match for No, and assigning the result to the variable named hopeful. Putting the /bin/mail piped into the grep command inside single back-quotes causes the shell to execute those commands and return their output; this output is what gets assigned to the variable hopeful.
