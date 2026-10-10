+   o [file-name]	Appends a copy of the current message to an Rmail-format file. This procedure can be used to create the equivalent of folders in other e-mail programs, collections of messages with a common subject origin.

+   Ctrl-o [file-name]	Does the same thing as o, except that the message files are saved in the standard mailbox format. Use this command if you want to be able to read these messages with another e-mail client, Emacs-based or independent.

+   w [file-name]	Copies the body of the current message to a new text file, stripping away all header lines in the process. The contents of the Subject: header will appear in the minibuffer as a default choice for a file name, giving you an opportunity to edit it or substitute another name.

Labeling messages lets you define your own categories that might be unrelated to subjects or sender. This gives you some of the advantages of separate mail files while still retaining your messages in a single file. When a message has been assigned a label, it is visible in the Summary buffer. These two commands assign and remove labels:

+   a [label]	Assigns a label to the current message. After you press a, the minibuffer becomes active. After you have typed a label, press Enter for it to take effect.

+   k [label]	This command is like a, but it removes a message's label instead.

Once you have given a group of messages the same label, you can use some new commands:

+   Ctrl-M-n [label1, label2]	Moves to the next message with the one of the listed labels. If no labels are specified the most recent label used with this command is re-used.

+   Ctrl-M-p [label1, label2]	The same as Ctrl-M-n [label1, label2], but moves backward.

+   Ctrl-M-l [label1, label2]	Creates a new Summary buffer displaying only those messages with the specified comma-separated labels.