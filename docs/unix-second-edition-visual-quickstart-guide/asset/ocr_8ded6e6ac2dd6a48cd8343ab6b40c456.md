![](bbox=[0.07, 0.11, 0.38, 0.3])

Figure 11.14 All you have to do is tell Unix where you want your messages forwarded to.

# Tips

+   - Check with your system administrator to see if a .forward file will really do what you want. Many newer Linux and Unix systems automatically send mail to procmail (and ignore the .forward file), so you might need to use a procmail recipe to forward your mail. It’s equally effective, but just different. See the section on procmail later in this chapter for details.
+   - If you want, you can keep a copy of all incoming messages (in your incoming email box, just where they’d usually be) and forward them to unsuspecting recipients. Just type yourid, otheraddress.com (filling in your userid on the current system for yourid and the address to which to forward the mail for the other one).
+   - Forwarding messages is also handy when you change ISPs. You can forward all messages sent to your old address to your new one, which helps tremendously in ensuring that you receive all your important messages while your friends and co-workers update their address books.

# Forwarding Incoming Messages

Suppose you’re the boss of a big project, and everyone sends you all the important related email messages. You can tell Unix to automatically forward these incoming messages to the people who will actually do something about them. Hey, you’re the boss, right? Or maybe you just got a different email account, and you want to forward all of the incoming mail sent to your old address to your new address. As Figure 11.14 shows, all you have to do is create a .forward file.

# To forward incoming email messages:

+   1. vi ~/.forward
+   To begin, type vi at the shell prompt (or the appropriate command for whichever editor you are using), indicate your home directory (with ~/), and then put .forward as the filename.
+   2. mynew@raycomm.com
+   Add, as the first line of the file, the address to which you want your email forwarded (Figure 11.14). In addition to forwarding to a single address, you can also use a .forward file with multiple addresses on multiple lines to send incoming email to several addresses at once.
+   3. Save and close the file.
+   Check out Chapter 4 for details about saving and closing files using pico or vi.