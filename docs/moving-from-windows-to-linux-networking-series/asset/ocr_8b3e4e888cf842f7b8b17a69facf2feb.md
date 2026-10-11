| [abc] | This means containing any of the characters listed. [abc]??? . txt means all text files that start with an a, b, or c followed by three characters. | 
|---|---|
| [a-m] | This means any character in the range shown. [a-l]?? . txt means any file starting with some letter from a to e, followed by two characters. |

Let's put some of these wildcards you just learned to good use and put them in a script. Open your favorite text editor and enter the following text:

```
#!/bin/sh
ls *.txt
ls [a-m]??? .txt
ls ?? .txt
exit 0
```

Now save this script in the same manner as you did the previous script. Make sure the file type is set to All Files and save it with the name scripttwo.sh . Then from the shell enter bash scripttwo.sh . You should see a display similar to the one shown in Figure 20.6 . Obviously, your display will depend entirely on what text files are in your directory. If you like, you can save blank documents with various names in this directory, just so you can test the script.

![](bbox=[0.06, 0.38, 0.65, 0.57])

Let's examine this script in some detail to make certain you understand it completely. The first line of the script is the same as in the first script we examined. In fact, all of the scripts we work with in this book will begin in this manner. What we see next are three separate calls to the ls command. The first uses the asterisk wildcard to ask for all files, regardless of their name, that end in .txt . This will display all text files in that directory. The second line says to display all files that begin with some letter from a to m, followed by three more letters and ending in a .txt . extension. The third line asks for all text files whose names have only two letters. Finally, we come to the exit 0 line, which instructs the script to exit.

This second example shows two things. First, it should demonstrate that writing scripts is not particularly hard. Make certain that you always check your spelling and end your script with the exit 0, and everything should be fine. The second thing this script illustrates is the enormous flexibility you have with wildcards.