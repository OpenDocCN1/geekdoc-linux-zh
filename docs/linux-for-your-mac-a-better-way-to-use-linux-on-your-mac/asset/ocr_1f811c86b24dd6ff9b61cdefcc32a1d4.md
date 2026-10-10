For information on how to compose messages using mail, read its manual page. This command is a bare-bones way to read and reply to electronic mail, but its terseness and lack of features can actually be viewed as a unique quality. For example, you can quickly send a message with a subject line and separate file in the body of the message with a single command line, like this:

```
$ mail -8 "System Log Update" root@yourSystem.com </var/log/messages
```

This makes the mail command an ideal candidate for use in automation scripts and for other system administration duties.

# ## Using pine

The pine e-mail program was developed by the University of Washington to provide students with an interactive electronic mail and Usenet newsreader. This versatile program also includes a separate, easy-to-use text editor name picco, which, in turn, is used for composing and replying to mail. Start pine from the command line of the console or an X terminal window, like this:

```
$ pine
```

The program will then create a directory named mail in your home directory. Pine also uses a resource file named .pinerc that contains your username, your domain, your ISP’s mail server, and other information (such as program settings). After starting pine, configure that program by typing an s and then a c. You will then see its configuration screen. Edit at least the first four values for the following:

personal-name             = your personal name
current-domain            = your ISP’s domain
smpt-server               = your ISP’s outgoing mail server
mtmp-server               = your ISP’s news server

Use your cursor keys to scroll through the items, and then press a c to change an item. When finished, press s to exit the setup screen. You are now ready to read and reply to mail. Your changes will be saved in your .pinerc file.

> If you use multiple ISPs, you can create different resource files by first copying the default .pinerc file, and then saving the files with different names. You can then start pine and force the use of a specific set of resource settings like this: pine -f .mypinerc.

![](bbox=[0.78, 0.78, 0.96, 0.85])

When you retrieve mail and then launch pine, your messages are displayed in a list on the screen (as shown in Figure 9.17). Select a message by scrolling up and down the list with the Up and Down arrow keys, and then press Enter to read a message.