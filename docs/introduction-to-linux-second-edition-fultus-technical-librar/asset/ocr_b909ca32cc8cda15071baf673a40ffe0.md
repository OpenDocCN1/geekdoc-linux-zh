# ### 2.1.3 Text mode

You know you're in text mode when the whole screen is black, showing (in most cases white) characters. A text mode login screen typically shows some information about the machine you are working on, the name of the machine and a prompt waiting for you to log in:

```
```
RedHat Linux Release 8.0 (Psyche)

blast login:
```

```

The login is different from a graphical login, in that you have to hit the Enter key after providing your user name, because there are no buttons on the screen that you can click with the mouse. Then you should type your password, followed by another Enter. You won't see any indication that you are entering something, not even an asterisk, and you won't see the cursor move. But this is normal on Linux and is done for security reasons.

When the system has accepted you as a valid user, you may get some more information, called the message of the day, which can be anything. Additionally, it is popular on UNIX systems to display a fortune cookie, which contains some general wise or unwise (this is up to you) thoughts. After that, you will be given a shell, indicated with the same prompt that you would get in graphical mode.

# #### Don't log in as root

Also in text mode: log in as root only to do setup and configuration that absolutely requires administrator privileges, such as adding users, installing software packages, and performing network and other system configuration. Once you are finished, immediately leave the special account and resume your work as a non-privileged user. Alternatively, some systems, like Ubuntu, force you to use sudo, so that you do not need direct access to the administrative account.

Logging out is done by entering the logout command, followed by Enter. You are successfully disconnected from the system when you see the login screen again.

# #### The power button

While Linux was not meant to be shut off without application of the proper procedures for halting the system, hitting the power button is equivalent to starting those procedures on newer systems. However, powering off an old system without going through the halting process might cause severe damage! If you want to be sure, always use the Shut down option when you log out from the graphical interface, or, when on the login screen (where you have to give your user name and password) look around for a shutdown button.