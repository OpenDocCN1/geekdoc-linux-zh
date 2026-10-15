
You won't necessarily understand everything that's happening in these files right away. The key takeaway is that this is where you can make permanent changes to every aspect of a shell's profile, including environment variables, shell options, and even text and background colors.

### Task 2

Test this theory by adding a simple welcome message. Open `~/.bashrc` in your favorite editor and add the following line at the end of the file:

```
echo "Welcome, $USER! You've successfully modified the .bashrc file!"
```

Save and quit, exit the terminal, then open a new terminal, and you should be greeted with your message.

Note that this only applies to your user. If you wanted it to apply to a different user, you would have to modify that user's own `.bashrc` file. To apply it to all future users, you would edit `/etc/skel/.bashrc`, or `/etc/bash.bashrc` to apply it to all current (and future) users.

**Notes:**

An interesting environment variable to experiment with is `PS1`. Running `echo $PS1` will print out a confusing mess of special symbols, but simply running `PS1="$ "` will make it immediately apparent that this, in fact, what defines your prompt!
