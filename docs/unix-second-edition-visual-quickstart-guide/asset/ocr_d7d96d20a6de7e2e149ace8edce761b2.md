```
xmision> echo $PATH
/usr/local/bin:/usr/local/bin/X11:
/usr/openwin/bin:/usr/bin:/usr/ucb:
/usr/etc:/usr/local/games:/home/users/e/
-ejray/bin:
xmission>
```

Code Listing 8.20 Here's your new path statement!

5. Save the file and exit from your editor. Refer to Chapter 4 for help if you need it.

6. su - yourid
As you learned back in Chapter 3, this command starts a new log-in shell so you can test your changes before logging out.

7. echo $path
Display the current path environment variable. This should include the addition you just made. Lo and behold! There it is! (See Code Listing 8.20.)