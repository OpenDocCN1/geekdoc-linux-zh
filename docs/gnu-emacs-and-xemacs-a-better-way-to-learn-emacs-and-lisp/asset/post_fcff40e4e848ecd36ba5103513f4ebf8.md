
## Rmail Output and Labels

Rmail offers a nice variety of commands for dealing with messages. You can save messages to files in either standard UNIX mailbox format or in Rmail's Babyl format:

- **o** `[file-name]` Appends a copy of the current message to an Rmail-format file. This procedure can be used to create the equivalent of folders in other e-mail programs, collections of messages with a common subject origin.
- **Ctrl-o** `[file-name]` Does the same thing as `o`, except that the message files are saved in the standard mailbox format. Use this command if you want to be able to read these messages with another e-mail client, Emacs-based or independent.
- **w** `[file-name]` Copies the body of the current message to a new text file, stripping away all header lines in the process. The contents of the `Subject:` header will appear in the minibuffer as a default choice for a file name, giving you an opportunity to edit it or substitute another name.

Labeling messages lets you define your own categories that might be unrelated to subjects or sender. This gives you some of the advantages of separate mail files while still retaining your messages in a single file. When a message has been assigned a label, it is visible in the Summary buffer. These two commands assign and remove labels:

- **a** `[label]` Assigns a label to the current message. After you press `a`, the minibuffer becomes active. After you have typed a label, press Enter for it to take effect.
- **k** `[label]` This command is like `a`, but it removes a message's label instead.

Once you have given a group of messages the same label, you can use some new commands:

- **Ctrl-M-n** `[label1, label2]` Moves to the next message with one of the listed labels. If no labels are specified, the most recent label used with this command is re-used.
- **Ctrl-M-p** `[label1, label2]` The same as `Ctrl-M-n [label1, label2]`, but moves backward.
- **Ctrl-M-l** `[label1, label2]` Creates a new Summary buffer displaying only those messages with the specified comma-separated labels.

Rmail might not have as many extra features as VM or Gnus, but many Emacs users find it sufficient for their needs.

## The VM Mailer

Kyle Jones created and currently maintains the VM mailer for Emacs. It is available as a preconfigured XEmacs package. The XEmacs documentation recommends VM as a good choice for beginners, although the package is configurable and is powerful enough to be a favorite with many experienced users.

Here is a partial list of the features VM offers:

- Sending and receiving MIME attachments
- Creating and “bursting” message digests
- Many ways to organize messages
- Virtual folders
- Many menu commands
- Configurable toolbars (on XEmacs and GNU Emacs 21)

VM is very configurable, but unfortunately it has no Customize support. If you have become addicted to the ease Customize brings to Emacs package configuration, Rmail or Gnus might be a better choice. Changing VM’s defaults involves inserting Lisp variable statements in a file named `~/.vm`, which is read when VM starts up. The variables are well-documented in the VM Info files; they can be copied directly from the Info window and then pasted into the `~/.vm` file.

That being said, VM’s default settings are reasonable, so you might not need to change any of them.

### Installation

GNU Emacs users need to install VM as an external package, because it is not included in the Emacs distribution. Before doing this, it wouldn’t hurt to find out if your Linux distribution has a packaged version of VM available. If a package is available, it might save you some time compared to manually building and installing the source distribution.

You can find a copy of the VM sources on this book’s CD-ROM, in the directory `/cdrom/packages/vm`. Unpack the archive and look for a file called `README`, which contains step-by-step installation instructions. You need to edit the makefile so that the files will be installed where you want them. A subdirectory of your `site-lisp` directory would be a suitable home for the VM Lisp files. You could put them in `site-lisp` itself, but it's generally a bad idea to install large multifile packages directly in the `site-lisp` directory. This makes it difficult to keep track of your Lisp files if you ever want to uninstall or upgrade a package.

The `README` file also contains a set of Lisp autoload statements that can be copied and pasted into your `~/emacs` file.

### First Steps with VM

The first time you press `M-x vm` or select **Read Mail (VM)** from the menu (in XEmacs only), your primary inbox or mail-spool file is emptied. Remember to make a copy of your inbox in case you want to go back to your original mail program. The messages are transferred to `~/INBOX`, and the VM window appears.

The screen is split into two windows, as shown in Figure 17.4. The top one is a Summary buffer in which each message is given a single identifying line, and the bottom window displays a preview of the first unread message, or optionally the complete message.

The preview is just a display of the message headers that is intended to allow you to decide if you really want to read that message. Pressing the spacebar reveals the remainder of the message. Pressing the spacebar repeatedly pages through the message. Pressing `b` pages backwards. Note that these keys work while point is in the Summary window, so you don't have to move point and keyboard focus back and forth between the two windows.

![](img/c8827ea52a0796def3f6891892ed9d3a_366_0.png)

Many VM users would rather not have this previewing action, preferring that a message be displayed in full. This leads to the subject of VM's configuration file, a Lisp file named `~/vm`, which you will need to create if you want to change any of the default settings. Actually, any VM-related Lisp statements could go right into your `~/.emacs` file, but they are easier to deal with in a separate file. VM reads this file if it exists every time it is started up.

The variable that controls previewing is `vm-preview-lines`. The default value is 0, which means that only the headers are previewed. A number larger than 0 causes that many lines of the message body to be displayed. The following statement disables previewing and forces VM to display the entire message when one is selected:

```
(setq vm-preview-lines nil)
```

In Figure 17.4, you can see that VM substitutes its own menus for several of the standard menus. You can switch back to the normal menus by clicking the XEmacs or Emacs button on the right side of the menu bar. When you do this, you see a VM button that toggles the VM menus' visibility.

### Sorting and Threading Messages

VM inherits many of its commands from Rmail, as you can see from the entries on the Sort menu, shown in Figure 17.5.

![](img/c8827ea52a0796def3f6891892ed9d3a_367_0.png)

These sorting commands are also available from the keyboard by pressing `g`. You are prompted in the minibuffer for one or more sorting criteria, such as subject or author. Press the Tab key twice, and a help window shows you all the valid choices.

A useful item on this menu is **Toggle Threading**, bound to `Ctrl-t`. It displays related messages in a hierarchical tree-like form, with later messages in a thread indented to the right.

### Message Digests

A digest is a message made up of many separate messages condensed into one. Many mailing lists offer subscriptions to a digest form of the list; this protects your inbox from a daily flood of list messages. You receive a single digest in their place.

VM has commands for “bursting” a digest into separate messages so that you can select and read them just as you would the normal messages in your mail folder. This makes it easier to respond to a particular message in the digest, because you can quote just the relevant message rather than the digest message itself. Typing the asterisk character splits the current message (if it is a digest) and merges the messages into your mail folder. If you click the middle mouse button on a digest message in the Summary buffer, the header is displayed in the message window, along with an icon representing the digest messages, as shown in Figure 17.6. Clicking again on the remainder of the message.

![](img/c8827ea52a0796def3f6891892ed9d3a_368_0.png)

*Figure 17.6 Expanded Digest Summary*
