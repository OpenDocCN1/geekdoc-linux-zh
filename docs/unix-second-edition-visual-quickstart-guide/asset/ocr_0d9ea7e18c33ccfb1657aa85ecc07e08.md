# Accepting Input While a Script Is Running

In the previous section, we showed you that you can require that information be provided along with the script in order for the script to run, but it’s easy to forget to input the information and thus not get the results you expected. You can also require input while a script is running. The script runs, you input some information, and then the script continues (probably) using the information that you input (Figure 10.8). In this case, the script counts misspelled words, but you can apply it to anything you want.

![](bbox=[0.62, 0.13, 0.92, 0.42])

Figure 10.8 You can also input information while a script is running.

# To accept input while a script is running:

+   1. pico retentive
+   Use your favorite editor to edit your script.
+   2. echo -e "Which file do you want to analyze?"
+   Specify the text for the prompt that you’ll see onscreen. Here, the onscreen text will read "Which file do you want to analyze?"
+   3. read choice
+   At whatever point in the script you want the script to accept information, type read followed by the name of the variable to accept the input. Here, we name the variable choice.
+   4. echo "Choice has `cat $choice | spell | wc -l` misspelled words"
+   Echo a phrase (and embedded command) to check the spelling, count the misspelled words, and report the number for the file specified. At each place where the filename should appear, substitute $choice.