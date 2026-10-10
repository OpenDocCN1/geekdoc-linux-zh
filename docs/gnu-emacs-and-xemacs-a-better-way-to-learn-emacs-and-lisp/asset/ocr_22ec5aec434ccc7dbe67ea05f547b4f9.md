ASCII messages was an achievement. Today there are still many e-mail users who have little need for MIME attachments and who value a simple and uncluttered interface. Because of these users, Rmail survives. If your needs aren't complicated and you don't mind having your mail stored in an incompatible format, Rmail might be what you need.

# The Babel Mailbox Format: a Warning

Rmail stores mail in a unique format called Babel, a format understood by no other mail software. You can try out Rmail, and if you decide it meets your needs, everything is fine. If you later decide to switch to an e-mail program or Emacs mode that uses the standard Linux mailbox format (in which all messages are concatenated into a single file), a command is provided to translate Babel mail files into the more widely used format. Press M-x and type

```
```unmail file-name```
```

This leaves the original Babel file alone while creating a new mailbox-format file from the contents.

XEmacs doesn't have the unmail command, and the documentation is vague about converting Babel files. XEmacs users are therefore advised to stick with Gnus or VM. Rmail is fully documented in the GNU Emacs Info files but is given nothing but a brief mention in the XEmacs Info files.

Probably the main reason so many users have migrated to VM or Gnus from Rmail is Rmail's lack of support for e-mail attachments. Once seen as unnecessary frippery, MIME attachments are now being used by the majority of e-mail users. If you feel that you will need to attach image files, Microsoft Word documents, sound files, or any other non-ASCII file to your messages, you should skip ahead to the VM or Gnus sections.

There is at least one third-party Rmail extension which adds attachment capabilities. It is called etach; you can learn more at http://etach.sourceforge.net/.

# Using Rmail

Start an Rmail session by pressing M-x and typing

```
```rmail```
```

or by selecting Read Mail from the Tools menu. The first thing Rmail does is move any messages from your inbox file (usually /var/spool/mail/your-user-name)