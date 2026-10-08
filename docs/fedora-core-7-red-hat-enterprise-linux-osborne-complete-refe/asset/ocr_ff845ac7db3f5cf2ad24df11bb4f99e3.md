found on all Unix and Linux systems. Mutt is a cursor-based client that can be run from the command line.

> **NOTE** You can also use the *Emacs* mail client from the command line, as described in the previous section.

# Mutt

Mutt has an easy-to-use screen-based interface. Mutt has an extensive set of features, such as MIME support. You can find more information about Mutt from the Mutt Web site, **www.mutt.org**. Here you can download recent versions of Mutt and access online manuals and help resources. On most distributions, the Mutt manual is located in the `/usr/doc` directory under Mutt. The Mutt newsgroup is **comp.mail.mutt**, where you can post queries and discuss recent Mutt developments.

# Mail

What is known now as the Mail utility was originally created for BSD Unix and called, simply, mail. Later versions of Unix System V adopted the BSD mail utility and renamed it mail. Now, it is simply referred to as Mail. Mail functions as a *de facto* default mail client on Unix and Linux systems. All systems have the mail client called Mail, whereas they may not have other mail clients.

To send a message with Mail, type `mail` along with the address of the person to whom you are sending the message. Press ENTER and you are prompted for a subject. Enter the subject of the message and press ENTER again. At this point, you are placed in input mode. Anything typed in is taken as the contents of the message. Pressing ENTER adds a new line to the text. When you finish typing your message, press CTRL-D on a line of its own to end the message. You will then be prompted to enter a user to whom to send a carbon copy of the message (Cc). If you do not want to sent a carbon copy, just press ENTER. You will then see EOT (end-of-transmission) displayed after you press CTRL-D.

You can send a message to several users at the same time by listing those users' addresses as arguments on the command line following the `mail` command. In the next example, the user sends the same message to both **chris** and **aleina**.

```
```
$ mail chris aleina
```
```

To receive mail, you enter only the `mail` command and press ENTER. This invokes a Mail shell with its own prompt and mail commands. A list of message headers is displayed. Header information is arranged into fields beginning with the subject of the message and the message number. The status of a message is indicated by a single uppercase letter, usually **N** for *new* or **U** for *unread*. A message number, used for easy reference to your messages, follows the status field. The next field is the address of the sender, followed by the date and time the message was received, and then the number of lines and characters in the message.

The last field contains the subject the sender gave for the message. After the headers, the Mail shell displays its prompt, an ampersand (`&`). At the Mail prompt, you enter commands that operate on the messages. An example of a Mail header and prompt follows:

```
```
$ mail
Mail version 8.1 6/6/93. Type ? for help.
"/var/spool/mail/larisa": 3 messages 2 unread
```
```