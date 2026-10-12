**PART III**

# talk

Writing to a device with `write` or `wall` is strictly one-way communication. One-way communication has benefits as well as drawbacks. For example, what if the person receiving the data wants to respond to the message? She could use a series of `write` commands or the `talk` command. The `talk` command notifies the second person that you want to talk. The command tells the other person what to type in order to finish initializing a `talk` session.

When the session is established, each person receives a split window. When the first person types information on the top window, it is echoed in the bottom window of the second person’s display and vice versa. Also, displaying in both windows happens as each letter is typed. As one person types, the other person sees the information.

# msg

The `msg` command was briefly mentioned in the discussion on `write`. The `msg` command is used to allow or disallow others from writing or walling messages to you. Of course, `root` overrides the `msg` authority. The syntax for this command is `msg y` or `msg n`. The `y` parameter allows the communication, and the `n` parameter disallows the communication with normal users.

# motd

`motd` (*message of the day*) is a good way to pass information on to whomever happens to log in that particular day. Typically, it is a reminder or an announcement of some type. Many companies use it to announce birthdays and other days of significance or to remind users of an event or telephone number to call. `motd` is a good way to communicate if the information is either not that important or only important to a person if he or she has logged in.

`motd` is actually a file that has its contents displayed upon login. The file is kept in the `/etc` directory and is called `motd` (`/etc/motd`). For example, when I log in to my computer, I receive the following message:

> The system will be down tomorrow for a hardware upgrade.  
> Hope you are having a great day!

![](bbox=[0.08, 0.8, 0.92, 0.82])

`motd` is only seen with a command-line login. This message of the day will not be seen if the user is logging in graphically as with KDE or GNOME.