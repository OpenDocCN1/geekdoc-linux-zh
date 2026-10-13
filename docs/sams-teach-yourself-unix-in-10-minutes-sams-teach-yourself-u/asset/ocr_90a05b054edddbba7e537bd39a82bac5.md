that don’t involve putting commands in files at all. One of the commands used for this is the foreach command.

# EXECUTING A COMMAND OVER AND OVER

If you find yourself in a situation where you need to repeatedly execute some action for each file in a set of files, the foreach command can help. It takes a list of files, and does something "for each" of them. The use is much easier to demonstrate than to explain. If you have a list of files that you need to do something to, you can follow these steps to use foreach:

+   1. Figure out what you want to do. In this example, you’ve got a bunch of directories, and you want to create a tarfile of each.
+   2. Decide on the names of the files/directories that you want to do your something to. In this case, you’re going create tarfiles for the directories mydirectory, yourdirectory, and herdirdirectory.
+   3. Pick a variable name that you want to use; here you’re just going to use a variable named test. It doesn’t much matter what the variable name is, just so long as it doesn’t conflict with the name of the command.
+   4. Issue the foreach command as foreach <variablename> (<filenames>). The foreach command then asks you what you want to do for each file by displaying a question mark. Fill this in with whatever you need to do. Again, you’re going to be tar ring files in the example. After giving foreach the command for whatever it is you want to do, finish it by putting the command end on a line by itself.

To illustrate the example, type the following:

```
> foreach test (mydirectory yourdirectory herdirdirectory)
? tar -cvf $test.tar $test
? end
```

Your machine will respond by running the tar command for each file you gave it to work with. Inside the foreach command loop, note the use of the expression $test. foreach goes through the list of filenames you gave it and puts each one sequentially in the test variable. To use the contents of a variable in the shell, put a $ sign before it. For example, foreach first