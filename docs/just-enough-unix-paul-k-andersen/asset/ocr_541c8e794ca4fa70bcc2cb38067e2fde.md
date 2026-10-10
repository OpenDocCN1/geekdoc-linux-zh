# 21.14 Exercises

+   1.  The date command prints the date and current time. Add the following line to your .profile, making sure to use backquotes around date:
+   
+       `echo "The date and time are `date`."`
+   
+       Exit the editor and run the .profile using the "dot" command. What happens?

+   2.  The backquotes were needed in the previous exercise to tell the shell that date was to be interpreted as a command, not as a word. What happens if the backquotes are omitted? Try it. Open .profile and remove the backquotes from date:
+   
+       `echo "The date and time are date"`
+   
+       Exit the editor and run the .profile using the "dot" command. What happens? (Now open up the file and replace the backquotes.)

+   3.  What is your search path?

+   4.  What is the complete pathname for your shell?

+   5.  The rm, cp, and mv commands are dangerous because they can overwrite or remove existing files. The -i ("interactive") option will ask you to confirm that this is what you want. If this option is available to you, add the following lines to your .kshrc file:
+   
+       ```
+       alias -x rm="rm -i"
+       alias -x cp="cp -i"
+       alias -x mv="mv -i"
+       ```

+   6.  Explain what the following lines would do if they were placed in your .kshrc file:
+   
+       ```
+       alias -x m=more
+       alias -x f=finger
+       alias -x ls="ls -R"
+       ```

+   7.  Most users set up their history mechanism to remember about 100 commands. To do this yourself, open your .kshrc file and insert this line:
+   
+       `HISTSIZE=100`
+   
+       If you neglect to set the HISTSIZE variable, ksh will remember the most recent 128 commands by default.