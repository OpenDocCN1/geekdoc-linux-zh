# # It's coming from inside the house

The simplest problems to fix are those that stem from a typo or a dangling wire in your computer room. If you configured Kppp and your modem according to the steps earlier in this chapter and yet you still don't get a connection, look through this list and try these solutions:

+   - Does the modem dial?
+   - If you don't get a dial tone, you may have a modem configuration problem. Get out your modem manual and redo the modem steps, paying careful attention to the `init` string.
+   
+   You should also check whether you have a phone line plugged into your modem. (It's one of those things that make you smack your head and say "D'oh!" just like Homer Simpson, but it's more common than you'd think.)
+   
+   - Does the modem dial, but fail to make a connection?
+   
+   Check to see if you entered the phone number for the ISP's modem bank correctly. If you have the right phone number, give your ISP a call. It may be a problem on their end, and you'll have to wait until it's fixed.
+   
+   - Does the modem make a connection but refuse to let you sign on?
+   
+   Did you enter your username and password correctly in the login script? Remember that usernames and passwords are case sensitive, so keep upper- and lowercase letters where they belong.
+   
+   - Are you receiving strange messages from the ISP after you sign on, especially things about DNS lookup failures?
+   
+   Make sure you entered all those IP numbers correctly. If that doesn't solve it, call your ISP. Be prepared to recite the error messages exactly as they appeared on your screen.

# # Knotted up in the Net

Sometimes you run into a problem that you simply don't know how to solve. It's not a problem with your own setup or with your ISP, but a problem with the great big beautiful world of the Internet. Because the Internet is a big old mess of networked computers, there are inevitably times that part of it won't work quite right.

When you're pretty sure you have an Internet connection problem, use KDE's basic network utilities to figure out what's wrong — or at least to get better information about what may be happening. The network utilities included with KDE are the same tools used by every network administrator and Internet expert. If you're having trouble, ping the problematic computer or run a quick traroute before you ask for help. Having that data ready to go will make you look quite smart and speed up the search for a solution.