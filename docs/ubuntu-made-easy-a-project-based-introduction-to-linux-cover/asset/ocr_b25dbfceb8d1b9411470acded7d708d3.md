Freenede, the IRC server used by Ubuntu (Figure 21-12). Now, type /ns register password email into the message box, replacing email with your email address and password with a good password. For example, typing /ns register nopeekingjane@example.com would do this if your details were details. Press ENTER to finish the registration.

![](bbox=[0.219, 0.166, 0.88, 0.473])

Figure 21-12: registration of your IRC nickname

If everything went to plan, you'll see a message saying something like An email containing nickname activation instructions has been sent to jane@example.com. Check your email, and there should be an activation email containing instructions to type something like /msg NickServer VERIFY REGISTER nickname jzq into the Freenode channel you were in earlier. Do this, and you will see a message along the lines of /NickServer- nickname has been verified. That's it, registered! Click the #ubuntu channel in the left pane to return to where you were.

If you get a message saying nickname is already registered instead of the one about an activation email, someone has already registered the nickname you're using. In this case, type /nick newname, replacing newname with a new choice of nickname, and you'll see a message that says You are now known as newname. Ideally, no one else has the name this time, try to register again.

The next time you go on IRC, you can retrieve your registered nickname by going to the freenode channel, typing /nick nickname, and pressing ENTER. Then type /msg NickServ identify password and press ENTER again. Of course, you should replace nickname and password with your own nickname and password word when you do this.