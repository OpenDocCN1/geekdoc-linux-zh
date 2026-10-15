# Importing Files into vi

You can also merge multiple files in vi by reading additional files into the current one, as shown in Figure 4.13. Basically, all this means is that you insert one file into the file you're currently editing.

# To import files in vi:

+   1. vi hairyspider
+   
+      At the shell prompt, type vi followed by the filename to start vi with, in this case, the hairyspider file.
+   
+   2. Esc :r filename
+   
+      At the point in the file where you want to import text, press Esc, then type :r and the filename you want to read into the file.

# Tip

vi also lets you read the output of commands into the file. For example, if you want to read the list of files in a specific directory into the file, use Esc :r !ls in command mode.

![](bbox=[0.58, 0.07, 0.92, 0.44])