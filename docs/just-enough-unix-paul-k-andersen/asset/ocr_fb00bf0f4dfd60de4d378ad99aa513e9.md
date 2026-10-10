USING SH OR KSH STARTUP FILES
21.4 Making Backups of the Startup Files

# 21.4 Making Backups of the Startup Files

The first step in creating a .profile is to see whether you already have such a file. If so, you should prepare a backup copy.

+   1. If necessary, go to your home directory. Remember, the cd command without arguments will take you to your home directory:
+      $ cd (Return)

+   2. List all files in your home directory. Enter the ls -a (“list -all”) command:
+      $ ls -a (Return)

If you see a file named .profile it means that one was placed in your home directory when your account was created. You may want to consult with your instructor or system administrator before editing this file. If you are a ksh user, also note whether you already have a .kshrc file.

+   3. Make a backup copy of the existing startup file(s).
+      $ cp .profile .profile.BAK (Return)
+      $ cp .kshrc .kshrc.BAK (Return)

# 21.5 A Login Message

In this section you will create a .profile file (or edit an existing file) to display a message on the screen every time you log in. You will use the echo command to do this.

+   1. Try out the login message. Type
+      $ echo "Your wish is my command, Oh Great One." (Return)

The shell should respond with the appropriate message:
Your wish is my command, Oh Great One.

+   2. Use your text editor to open the .profile file.
+      $ vi .profile (Return)

+   3. Insert a comment showing the modification date. Put the following line at the top of .profile:
+      # This file was last modified on [today's date].

The # at the beginning of the line makes this a comment. This shows a typical use of comments, which is to tell you when the file was last edited.

+   4. Add the message command to the file.

233