
It is best to just start here and follow the links to the latest release to install. The installation happens right in your browser. Depending on how you have Mozilla or Firefox installed, you might have to run your browser as the root user to get ChatZilla installed. If you're not sure, run the program as root.

## Run as Root

What's the easiest way to run a GUI program as root? The terminal, of course, is the best method, for example:

```bash
$ su
Password:
# mozilla &
```

Don't forget, the ampersand at the end of the command runs the program in the background, keeping your terminal free for more commands.

When you have the program installed, you need to restart your browser. Close and open Mozilla or Firefox, and then take a look in the menu. In Mozilla, go to Window > IRC Chat. In Firefox, go to Tools > ChatZilla. Firefox also gives you the option to add ChatZilla as a toolbar button.

1.  Open ChatZilla (see Figure 10.8).
2.  The initial screen that you will see is full of “[INFO]” blurbs. Among those are a list of available networks. Just pick one of those: Click freenode to start.
3.  You are prompted for a nickname. Enter one and click OK. Pick something that won't embarrass you later in life.
4.  Lots more messages scroll through. If you have successfully joined the server, you should see something like this at the end of all the other info:
    - `-- End of /MOTD`
    - `== User mode for [your user name] is now + i`
    - The MOTD is the message of the day. That's what a lot of the text that scrolled past was. Just scroll up in the window to read it—some of them are pretty funny.
5.  Now you need to find a channel to join. A channel is like a room full of people to talk to. To list active channels, type this:
    - `/list`

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_272_0.png)

The list you get back on a big server such as freenode.org can be long. You can limit the number of channels you get listed back by using the `-min` and `-max` options:

```bash
/list -min 5
```

This returns channels with at least five people in them. You can also go to http://www.irchelp.org/irchelp/channelist to see some search engines to find channels.

### Figure 10.8
ChatZilla.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_273_0.png)

6.  On Freenode.net, you can probably enter the channels `#newirc` and `#newsr` and not get into too much trouble. You join a channel with the `/join` command:

    ```bash
    /join #newsr
    ```

    Don't be surprised to find yourself the only one in the channel. If so, that's okay; just practice some of the commands and maybe emote some poetry to yourself.

7.  To talk, just type and click Enter. To emote, use the command `/me` and then finish the sentence. For *example*:

    ```bash
    /me is a genius
    ```

    comes out when I am logged in as

    ```
    ** susan is a genius
    ```

8.  To leave, use `/leave`.

## A Few Basic IRC Commands

Table 10.1: IRC Commands

| IRC COMMAND | RESULT |
|---|---|
| /help | Displays help info from that server, which can be a long listing |
| /join #philosophy | Joins the channel named philosophy |
| /leave or /part | Leaves the channel, but stays in the server |
| /list | Lists channels on the server |
| /me dances like a cowboy | ** [your username] dances like a cowboy |
| /msg josh | Sends a private message to the user with the nickname josh |
| /nick newnickname | Changes your username—to newnickname, in this case |
| /invite | Invites another user to a channel |
| /quit see ya | Quits IRC and sends the parting message "see ya" |

## XChat

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_274_0.png)

Every group of programs has the solid, reliable veteran. For IRC chat, that solid program is XChat. If you are new to IRC, XChat is probably your best choice because it makes everything easy for the newbie. As soon as you start XChat, you see a few simple fields to fill in your username (it defaults to your Linux username) and a list of servers to join. Choose a server, and the main XChat window pops up.

In the main window (see Figure 10.9), you see the chat side on the left, a place for commands on the bottom, and a user list on the right. The menu is full of options to help you if you don't know the corresponding IRC commands for those actions, or if you just don't feel like typing them in. The Server menu has Join Channel and Leave Channel among its options. Under the Settings menu, you can even learn some new IRC user commands by browsing through the list in Settings > Lists > User Commands.

### Figure 10.9
XChat's main window.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_275_0.png)

After you connect to a server, use /list to find a channel, or search for one online, and then use /join #channelName to join. You will probably not have any technical problems while using XChat—just some possible people problems. Be polite, play nice with the other kids, and make sure you're home in time for supper.

## The Skinny

| Program | Usability | Interface | Comments |
| :--- | :--- | :--- | :--- |
| Gaim | Great | Good | Gaim does it all. Just like many GNOME/GTK programs, it lacks some of the design and feature bells and whistles of its KDE counterpart, but it makes innovations in function. The Gaim developers have regular releases and are among the most responsive when it comes to fixing reported bugs. Having a parallel Windows version means that you can keep the same program and interface even if you have to use Windows for some reason. Also, the program is self-contained and can run equally well in KDE and GNOME |
| Kopete | Good | Great | Kopete started off slow but has caught up to Gaim in most respects, while adding a few twists of its own. If you are a regular user of the KDE desktop, the integrated features Kopete uses with KAddressBook, the system tray, and KNotify will be great |
| Yahoo! Messenger | Good | Fair/poor | You won’t ever have to worry about not being able to connect to Yahoo’s changing protocols when you are using their client, but you won’t have as many features, either. It’s admirable that Yahoo! has cared enough to make a Linux version of their IM program, but it would be nice if they kept it up-to-date. Not only does the interface look old compared to other Linux programs, but it doesn’t even keep up with the features that Yahoo’s client for Windows has. This one is good to keep on hand as a backup. |
| ChatZilla | Fair | Fair | ChatZilla is a fairly new program that Mozilla lists as not finished yet. The program is one of those that works just fine but has no fun toys in it to play with. The fact that you can launch it right from your browser is convenient. |
| XChat | Good | Good | XChat is made only for IRC chat, and that's what it does well. The built-in server list and well-planned menu choices make this the most straightforward and easy IRC client to use. |

## Links

- Jabber: http://www.jabber.org/
- Jabber server list: http://www.jabber.org/user/publicservers.php
- Gaim: http://gaim.sourceforge.org
- Gaim's SourceForge Forums: https://sourceforge.net/forum/?group_id=235
- Gaim-festival (speech add-on for Gaim): http://festival-gaim.sourceforge.net/
- Gaim's plug-ins: http://gaim.sourceforge.net/plugins.php
- Kopete: http://www.kopete.org/
- Yahoo! Messenger: http://messenger.yahoo.com/
- ChatZilla on Mozilla.org: http://www.mozilla.org/projects/ir-messaging/chatzilla/
- ChatZilla user's guide: http://www.mozilla.org/projects/ir-messaging/chatzilla/user-guide.html
- XChat: http://www.xchat.org/
- IRC help page: http://www.irchelp.org/

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_278_0.png)

# Music and Movies

Some people are truly busy people. Most of the rest of the busy people fall into two categories. There are the people who like to say they are busy because it makes them feel important. These busy people are the ones who often tell you how little sleep they get, how much driving around they have to do, how many projects they are going on. They boast so that you will then think that these busy people are special people who are so needed that they can't even sit down for one minute. Then there are the busy people who say they are busy so that they can get out of doing what they are supposed to do. These busy people are the ones who don't speak up until they are asked to do some unpleasant task or to attend an unwanted social function. Suddenly, they are so busy.

“Honey, are you ready to help me clean the car?” my husband called out one afternoon.

I looked around the room for some saving grace, some out. All I was doing was watching a movie on my computer and organizing my MP3 collection.

“Susan?” he repeated.

I needed an answer. “I'm sorry, I can't. I'm really busy right now.” Guess which kind of busy person I am.

“What are you doing?” he asked.
