# Question 7

How would you check the spelling of a document edited through the vi editor?
The name of your document file is important.txt.

+   - a. Open vi. Go into command mode. Type the s command to start the spell checker.
+   - b. Open vi. Go into command mode. Type the ispell command to start the spell checker.
+   - c. Go to your command-line interface. Type the ispell important.txt command.
+   - d. Go to your command-line interface. Type the vi important.txt | ispell command.

Answer c is correct. The ispell command works on any text file and is independent of the editor. The s command in vi deletes the current character and brings vi into insert mode; therefore, answer a is incorrect. The ispell command is used at the command-line interface; therefore, answer b is incorrect. Because the vi command opens that editor, the "pipe" (|) has nothing to send to the ispell command. Therefore, answer d is incorrect.