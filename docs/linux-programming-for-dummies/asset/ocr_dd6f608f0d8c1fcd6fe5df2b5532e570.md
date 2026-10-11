+   1. Move to the directory that contains your file if you're not already in that directory by typing the following command at the prompt:
+   
+   cd /mydirectory
+   
+   Remember to replace mydirectory with the directory name on your computer that contains your program file.
+   
+   2. Make the file an executable file by using the chmod utility, typing the following at the command prompt:
+   
+   chmod 711 mymenu
+   
+   This command enables everyone to run your mymenu program — but only you can see the file itself. (Refer to Chapter 1, where I explain a little about the chmod utility.)
+   
+   3. You can run your program by typing the name of the program at the command line as follows and then pressing Enter:
+   
+   mymenu
+   
+   If you have problems running your mymenu program, try running the program as . /mymenu.
+   
+   The program displays the menu on-screen and prompts you to enter a selection from the menu. After you enter your selection, the program ends.

# Making changes to your program

You can change your program at any time by recalling your program to the screen by using the vi text editor or the text editor of your choice.

Using vi as my model, for example, I simply type vi mymenu at the command prompt. Here I can start vi again and use the name of the program file. Remember that, after you first start vi, you're in the command mode.

Expect to edit your programs frequently. Always make another copy of your program under a different name before you begin changing your program. You can use this backup copy of your program in case you accidentally destroy your program during editing.