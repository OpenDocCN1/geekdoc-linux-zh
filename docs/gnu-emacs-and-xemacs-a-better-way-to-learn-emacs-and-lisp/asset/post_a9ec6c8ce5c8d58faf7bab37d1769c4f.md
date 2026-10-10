
to a different file format. This has happened to me a couple of times, and believe me, it's annoying! It is possible to convert mail from one format to another, but with a little foresight, you won't ever have to.

The best way to deal with this is to get into the habit of copying your mail-spool file to a temporary directory before you install any new mail client. You can move it back later if you decide to go back to your original e-mail setup.

## Writing E-Mail in Emacs

There are certain interrelationships between the different e-mail modes. Rmail and VM both use mail-mode, the basic mail-composition mode. VM expands upon mail-mode, giving it more power and flexibility. Gnus uses its own composition mode, known as message-mode.

mail-mode can be used by itself; you can compose and send messages without making use of the full-blown mail modes at all. You can continue to use another non-Emacs mail program for both receiving and sending mail.

Enter mail-mode by pressing `Ctl-x m`.

A Mail buffer appears, complete with a set of standard mail headers that can be edited, as shown in Figure 17.1.

![](img/c8827ea52a0796def3f6891892ed9d3a_358_0.png)

The Headers menu lets you insert optional headers that aren’t needed for every message, such as CC and FCC. As you can see in Figure 17.2, the keybindings are long, so using the menu is quicker. You might wonder why keybindings are even included at all, because not many users will bother to memorize them. One reason is that the developers have gone to great lengths to ensure that every command is available to users on simpler displays, such as the Linux virtual console. Emacs in a nonwindowed, nongraphical environment has no menu bar, though the menu items can be accessed by pressing F10. The great majority of Linux Emacs users run the editor in an X Windows session, ignoring complicated keybindings when a menu is available.

Nearly every e-mail program has an address book, because nobody enjoys repeatedly typing often-used e-mail addresses. mail-mode doesn’t have a graphical address book; instead, it uses the concept of mail aliases. Creating aliases is no more difficult than entering e-mail addresses in an address book window. All you need to do is create a file in your home directory and name it `.mailrc`. Enter one e-mail address per line, using a format modeled after either of these examples:

```
alias bank hdt.walden.net
alias jorge “Jorge Luis Borges <jborges@biblio.ar>”
```

Any address in an alias that includes spaces, such as the second one shown here, must be enclosed in double quotes.

When you enter mail-mode, Emacs checks to see if you have a `~/.mailrc` file. If one is found, it is read into memory. If that file contained the first of the preceding two imaginary entries, typing `bank` in the `To:` field would automatically be expanded to `hdt.walden.net` as soon as the message was sent. XEmacs does this a little differently. As soon as the cursor moves out of the `To` field, the real e-mail address is inserted. This is a worthwhile safety feature, because it lets you make sure that the alias points to the correct e-mail address.

Sending mail successfully requires that you have one of the available mail-delivery agents installed and configured. Sendmail and Exim are two of the most popular. Your Linux distribution will have chosen one of these (or possibly another) as the default. Current distributions almost always provide a mail setup program, often as a part of the installation process.

You type the message body starting on the line just below `--text follows this line--`. That line is a delimiter that separates the body of the message from the headers, but it doesn't appear in the message itself, because Emacs deletes it first.

Signatures (or sigs) are the lines you want appended to your messages—often a professional identification or a quote. If you want your default sig tacked on to the end of your message, the key command `Ctrl-c Ctrl-w` or the menu command **Insert Signature** will do this for you. This was left as an option because you might not want a sig on every message. Emacs uses the file `~/.signature` as the default signature file.

When you are ready to send the message, `Ctrl-c m` hands it over to your delivery agent. You don't have to be online, because the first destination of a message is a mail queue directory. Delivery agents typically “wake up” every few minutes and try to send the messages that have accumulated in this directory. If the mail server can't be found (meaning you aren't connected to the Internet), the agent will go back to sleep and try again later.

## Teaching Emacs Your E-Mail Address

Depending on how your Linux installation is set up, Emacs might or might not be able to figure out your name and e-mail address. Just to make sure, it is wise to insert a few lines into your `~/.emacs` file that set these variables permanently:

```
(setq user-full-name "Your Name")
(setq user-mail-address "youremail.address")
(setq mail-archive-file-name "~/Mail/emacs.sent")
```

The last line sets the location and file name of your archive of all messages that have been sent from Emacs. This file is the equivalent of the outbox file or directory used by other e-mail programs. The file can become gargantuan if you send many messages with attachments (only possible with VM and Gnus), so it is advisable to edit the file periodically and delete the portions you don't need to save.

Now that you can send mail with Emacs, receiving new messages involves using either Rmail, VM, or Gnus.

## Rmail for Basic E-Mail

Rmail is the oldest of the Emacs mail packages. It was developed in the early days of e-mail, when attachments were unknown and just being able to send and receive ASCII messages was an achievement. Today there are still many e-mail users who have little need for MIME attachments and who value a simple and uncluttered interface. Because of these users, Rmail survives. If your needs aren't complicated and you don't mind having your mail stored in an incompatible format, Rmail might be what you need.

### The Babel Mailbox Format: a Warning

Rmail stores mail in a unique format called Babel, a format understood by no other mail software. You can try out Rmail, and if you decide it meets your needs, everything is fine. If you later decide to switch to an e-mail program or Emacs mode that uses the standard Linux mailbox format (in which all messages are concatenated into a single file), a command is provided to translate Babel mail files into the more widely used format. Press `M-x` and type:

`unmail file-name`

This leaves the original Babel file alone while creating a new mailbox-format file from the contents.

XEmacs doesn't have the `unmail` command, and the documentation is vague about converting Babel files. XEmacs users are therefore advised to stick with Gnus or VM. Rmail is fully documented in the GNU Emacs Info files but is given nothing but a brief mention in the XEmacs Info files.

Probably the main reason so many users have migrated to VM or Gnus from Rmail is Rmail's lack of support for e-mail attachments. Once seen as unnecessary frippery, MIME attachments are now being used by the majority of e-mail users. If you feel that you will need to attach image files, Microsoft Word documents, sound files, or any other non-ASCII file to your messages, you should skip ahead to the VM or Gnus sections.

There is at least one third-party Rmail extension which adds attachment capabilities. It is called **etach**; you can learn more at http://etach.sourceforge.net/.

### Using Rmail

Start an Rmail session by pressing `M-x` and typing:

`rmail`

or by selecting **Read Mail** from the Tools menu. The first thing Rmail does is move any messages from your inbox file (usually `/var/spool/mail/your-user-name`) to `~/.RMAIL`, Rmail's default mailbox file. All messages are converted to Babyl format before the file is saved.

Rmail doesn't by default fetch new mail from wherever your e-mail comes from, such as a POP or IMAP server. This is up to you to set up. Many Linux users use Fetchmail to retrieve new messages. Both VM and Gnus can connect to mail servers and pull down new messages.

> The Rmail Info manual (in the section “movemail and POP”) describes the set-up necessary for connecting directly to a POP server for mail retrieval. Briefly, rather than using an inbox filename, an entry such as this is used:
>
> ```
> po: [username]:[mail hostname]
> ```
>
> You will be prompted for your POP password.

![](img/c8827ea52a0796def3f6891892ed9d3a_362_0.png)

Rmail mode redefines many of the letter keys so that they run message-related commands. Most have mnemonic values:

| Command | Description |
| :--- | :--- |
| `m` | Writes a new message (the recipient needs to be entered in the To: field). |
| `r` | Replies to a message. |
| `f` | Forwards a message to another address. |
| `d` | Marks a message for deletion. |
| `u` | Undeletes. |
| `x` | Expunges (actually deletes marked messages). |
| `s` | Saves a message to a file and then deletes it from the folder. |

The first three commands open a mail-mode window, as described earlier.

You create the Rmail Summary buffer by selecting one of the items on the Summary menu or using the keyboard equivalents. Pressing `h` makes visible a new window with all messages shown in chronological order. Rmail can sort and filter the messages in a variety of ways. Figure 17.3 shows a summary chosen with a regular expression, `LISTERV`. The menu in the figure shows the other message-filtering possibilities.
