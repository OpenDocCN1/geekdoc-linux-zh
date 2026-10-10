only the read permission. The first answer (`drwxrwxrwx`) might seem right at first, but it refers to a directory. The third answer (`x` and `rx`) is incorrect because of the word *and*. The last two answers are red herrings.

+   3. The recommended solutions are a) and c). It is considered best practice to define the variables inside the script and export them to make them available to subshells.
+   
+   4. At the beginning of the script file, use the `#!/bin/bash` statement. This action will ensure that the script will run the *bash* shell environment no matter what shell the user is in.
+   
+   5. The results of this script are false because `"foo" does not equal "bar."`
+   
+   6. The results are still false, because although you can set and even export the variables T1 and T2 at the command line when the script executes, it will set them right back to `T1="foo"` and `T2="bar"`. This situation is a common error in scripting, which is why you should always check the variables before you implement them.

# Chapter 14

+   1. Statements b), d), and e) are true. Regarding statement a), connections are based on TCP/IP. Regarding statement c), it is the definition of a server in non-Linux/UNIX environments.
+   
+   2. The `XF86` program (as configured by using the `XF86Config` file) with other software that helps `XF86` to control other functions and attributes of the `X` environment is the `X` Server for your system(s).
+   
+   3. *export*, along with another command and other options and arguments. A case could be made for including `telnet` as well because it too can be used to connect to other machines. Then, once connected, a user can execute clients on the remote system.
+   
+   4. `-bg red`: the background color of the new `xterm` window is red.
+      `-fg black`: the foreground characters are white.
+      `-T ledger`: the title of the window is `ledger`.
+      `-geometry 80x125+0+0`: make the window `80` pixels wide and `125` pixels long and place it in the upper-left corner of the root window.