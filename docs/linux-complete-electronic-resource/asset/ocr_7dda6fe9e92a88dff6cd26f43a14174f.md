before giving up. For a really slow server, you may need even more than this.

Alternatively, you can get a bit tricky in return. You may have noticed that when you logged in by hand to the PPP server and PPP started there, the first character of the PPP garbage that appears was always the tilde character (~). Using this knowledge we can add a new expect/send pair to the end of the chat script that expects a tilde and sends nothing. This would look like:

```
\~
```

![](bbox=[0.04, 0.29, 0.14, 0.38])

# NOTE

As the tilde character has a special meaning in the shell, it must be escaped (and hence the leading backslash).

# Default Route Not Set

If pppd refuses to set up a default route, it is because (quite correctly) it refuses remove/replace an existing default route.

The usual reason that this error occurs is that some distributions set up a default route via your Ethernet card as opposed to setting up a specific network route.

See the Linux NAG and the Net2/3 HOWTOs for information on correctly setting up your Ethernet card and associated routes.

An alternative to this is that your LAN uses a gateway/router already and your routing table has been set up to point the default route at this.

Fixing up this last situation can require a fair bit of IP networking knowledge and is beyond the scope of this HOWTO. It is suggested you obtain some expert advice (via the news groups or from someone locally you can ask).

# Other Problems

There are many reasons apart from these that PPP fails to connect and/or operate properly.

Look in the PPP FAQ (which is really a series of questions and answers). This is a very comprehensive document and the answers are there. From my own (sad) experience, if the answer to your problems is