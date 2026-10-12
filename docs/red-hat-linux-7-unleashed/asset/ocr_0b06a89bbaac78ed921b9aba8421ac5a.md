When you try to establish a talk link, you can also define to which terminal, or tty as they are often referred to in UNIX lingo, your request should be directed. To do this you simply add the name of the tty after the username. This can be useful if the user to whom you wish to chat is logged in with several terminal sessions.

# ## Chatting via Talk

After the talk session has been established your terminal screen will split into two parts. The upper part is where you will type text. Whatever you type will show up immediately on the recipient’s side. The lower part of the terminal window will show whatever the person to whom you are chatting is writing.

Typing certain control sequences serve as commands to the talk client. Table 7.1 shows the command sequences that are available while chatting. The scroll commands will only affect your side of the talk session.

The Meta key is usually assigned to your Alt key. You may also use the Escape key as a substitute for the Meta key. To do this, press the Escape key and then press the key that you want to combine it with. Please note that this will not auto repeat—so you will need to perform the escape combination repeatedly to scroll more than one line at a time.

**Table 7.1 Control Commands Used in Talk Sessions**

| Command | Description |
| :--- | :--- |
| Ctrl+c | Ends the talk session. |
| Ctrl+l | Redraws the screen. |
| Ctrl+n | Scrolls the upper text buffer down. |
| Ctrl+p | Scrolls the upper text buffer up. |
| Ctrl+u | Deletes the current row. |
| Ctrl+w | Deletes the current row. |
| Meta+n | Scrolls the lower text buffer down. |
| Meta+p | Scrolls the lower text buffer up. |

# ## Controlling Access to Your Terminal

Sometimes you might not want people to be able to interrupt you by requesting to talk to you. To avoid this you can use the **mesg** command to turn off external access to your terminal. There are two possible parameters for **mesg**: y or n. A y indicates that access is allowed, whereas an n is used to disallow access. Running **mesg** without any parameter will show the current state of your terminal. The default behavior of a new terminal is to have external access turned on.