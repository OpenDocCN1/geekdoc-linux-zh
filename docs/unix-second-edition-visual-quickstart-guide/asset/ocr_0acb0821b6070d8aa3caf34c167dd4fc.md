# Using Input to Customize Your Environment

Way back in Chapter 8, we talked about setting up your environment variables by customizing the configuration files that run upon log in. You can further customize your environment variables by requiring input whenever a startup script runs. For example, you can set your configuration files (which are actually scripts) so that they request that you specify the default editor for the session (Code Listing 17.5).

# To use input to customize your environment:

+   1. vi ~/.bash_profile
+   Use your favorite editor to edit your script, and move to the end of the file.

+   2. echo -e "Which editor do you want as the default? (vi or pico)"
+   Using echo -e, specify the text that will prompt you to input information (Figure 17.3).

+   3. read choice
+   On the next line, add read followed by the name of the variable to read in. We chose choice because we’re using this input to set the preferred EDITOR environment variable.

+   4. if [ $choice = "vi" ]
+   Start an if statement—in this case, one that tests for the vi option.

+   5. then EDITOR=/usr/bin/vi ; export EDITOR ; echo "You chose vi!"
+   Here, the then clause sets the EDITOR environment variable to vi, exports the environment variable, and announces your choice.

```
[ejr@hobbes ejr]$ su - ejr
Password:
Which editor do you want as the default?
(vi or pico)?
vi
You chose vi!
[ejr@hobbes ejr]$
```

Code Listing 17.5 When the system asks your preferences, you know you're on top.

![](bbox=[0.07, 0.4, 0.48, 0.65])

Figure 17.3 Add this mini-script to your .zprofile, .bash_profile, or .profile configuration file, right at the end.