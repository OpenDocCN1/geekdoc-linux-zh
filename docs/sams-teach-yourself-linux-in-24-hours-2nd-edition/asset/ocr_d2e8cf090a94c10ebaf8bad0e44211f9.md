But looking at several files is only one way to use cat. You can also use the cat command with the redirection operator (>) to combine files. For example, if you want to combine test.txt and test2.txt into a third file called test3.txt, you can use the following:

```
# cat test* > test3.txt
```

You can check the result as follows:

```
# ls -l test*
-rw-r--r-- 1 bball users 190 Jan  4 16:06 test.txt
-rw-r--r-- 1 bball users 108 Jan  4 16:07 test2.txt
-rw-r--r-- 1 bball users 298 Jan  4 16:07 test3.txt
```

But what if you want to combine test.txt and test2.txt without creating a larger, third file? In this case, you first decide whether you want the contents of test.txt to go into test2.txt or the contents of test2.txt to go into test.txt. Then, using cat with the >> redirection operator, you type the following:

```
# cat test.txt >> test2.txt
```

This appends the contents of test.txt to the end of the test2.txt. To check the results, use cat again:

```
# cat test2.txt
This is the first line of test2.txt.
This file was also created by cat.
This is the last line of test2.txt.
This text file was created by the cat command.
Cat could be the world's simplest text editor.
If you read this book, you'll learn how to use cat.
This is the last line of text in this file.
```

Note that you can instead enter the command as follows:

```
# cat -n test.txt >> test2.txt
```

![](bbox=[0.88, 0.55, 1.0, 0.68])