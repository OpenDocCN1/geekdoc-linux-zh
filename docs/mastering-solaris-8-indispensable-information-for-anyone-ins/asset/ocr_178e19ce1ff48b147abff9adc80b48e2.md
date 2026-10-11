to you and is not a copy. The code N means that the message is new. Code D means that the message has been marked for deletion.

If the message is from another user on your netwerk, you could use the following commands:

+   - R to reply
+   - F to forward the message to someone else
+   - S to save the message in a message folder
+   - D to mark the message for deletion

There are two steps to deleting a message. First, you mark the message for deletion, and then you enter Y and the message is deleted. You can delete messages at any time, and you will be queried when you quit pine about whether you want the messages marked for deletion to be deleted at that time.

If you are already in the mailer and want to read the messages in the default folder (INBOX), you can select the Folder Index option from the main menu and bypass the folder list on the screen. This is a time-saver when you want to read just the messages in your INBOX and not have to access all the folders on the list. There is also a convenient shortcut to enter the Folder Index screen from the command line:

```
$ pine -i
```

Again, you can send mail such as a memo to more than one person at a time. You can access the message composer directly by typing the following command at the shell prompt (this will send messages to all three users):

```
$ pine al dave jim
```

You will be able to send messages to users on other systems if your system is a part of a network. You need to know their login name and a machine name and type both separated by the @ character, such as in the following example:

```
$ pine barrie@reliable
```

To send a message over the Internet, you would also have to know the domain name but not necessarily the machine name, such as in this example:

```
$ pine barrie@sosinsky-group
```

# The pine Newsreader

There is also a news interface called pine, which is related to the pine mail interface. There is consistency between commands, screen displays, and folder organization, which makes the newsreader easy to use. If you use the Netscape browser, you can use Netscape News as well. However, you have the option of using pine as a