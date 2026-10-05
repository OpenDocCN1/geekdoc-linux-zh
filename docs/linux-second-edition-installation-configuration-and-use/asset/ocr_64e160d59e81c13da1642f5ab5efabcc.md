# slrn

According to the RedHat package description, slrn is the best news reader on earth! Before you share this opinion, you have to take a little time to get used to it. The great features are hidden behind an unyielding interface, even in the age of KDE Gnome gone without icons. It should suffice for a first approach.

Up-to-date information on slrn, including a very helpful collection of FAQs, can be found on the Internet:
http://space.mit.edu/~davis/slrn

# Start

Independently of whether the program is used for accessing a local server or an extremal server over the Internet, the server name must be set in the environment variable NNTPSERVER. Alternatively, the name can also be specified with -h. (The server name for the sample user from page 305 is news.provider.de If you use leafnode (described on page 380) for your local news server, the server name is simply locally.)

In order to start slrn, either .newsrc or .newsrc must be located in the home directory. If neither is the case (because so far no other news client has used), slrn issues an error message.

```
hofer slrn
rn 0.9.5.2 (Dec 11 1998 21:07:03)
Reading startup file /var/lib/slrn/slrn.rc.
Unable to open /home/hofer/.jnewsrc. I will try .newsrc.
slrn fatal error: Unable to open /home/hofer/.jnewsrc.
```

This problem is easily remedied. Try again, and this time you use the following options:

```
hofer slrn -f ~/.newsrc-create
srn 0.9.5.2 (Dec 11 1998 21:07:03)
Reading startup file /var/lib/slrn/slrn.rc.
Connecting to host localhost...
Connected to host. Posting Ok.
--The next step may take a while if the NNTP connection is slow---
Creating /home/hofer/.newsrc........
```

Reading the list of all stored newsgroups may take some time - but this is only needed at the first start-up.

slrn now shows a (still empty) list of all subscribed newsgroups. To display groups - including the ones you have not yet subscribed to - enter Shift+*
Instead of *, you can enter any pattern, such as *.os. for all newsgroups involving operating systems.