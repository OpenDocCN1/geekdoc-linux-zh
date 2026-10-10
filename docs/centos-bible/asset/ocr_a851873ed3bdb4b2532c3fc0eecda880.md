The mutt command is a text-based, full-screen mail user agent for reading and sending e-mail. The interface is quick and efficient. Type `mutt` to start the mail program. Click the up and down arrow keys to select from your listed messages. Press [Enter] to see a mail message, and type `1` to return to the Main menu.

The menu bar indicates how to mark messages for deletion or undelete them, saves messages to a directory, or reply to a message. Type `m` to compose a new message, and it opens your default editor (for me, `vi`) to create the message. Type `y` to send the message. If you want to read mail without having your fingers leave your keyboard, Mutt is a nice choice. (It even handles attachments!)

# Alpine Mail Reader

The Alpine mail reader is another full-screen mail reader, but it offers many more features than does Mutt. With Alpine, you can manage multiple mail folders. You can also manage newsgroup messages, as well as mail messages. As text-based applications go, Alpine is quite easy to use. It is developed by a group at the University of Washington for use by students on campus, but has become widely used in UNIX and Linux environments.

> **NOTE**
> The alpine package is not distributed with CentOS, but you can get Pine from the EPEL or RPMforge repositories.

Start this mail program by typing `alpine`. The following menu is displayed, from which you can select items by typing the associated letter or using up and down arrows and pressing [Enter]:

+   ```
+   ?  HELP                - Get help using Alpine
+   C  COMPOSE MESSAGE     - Compose and send a message
+   I  MESSAGE INDEX       - View messages in current folder
+   L  FOLDER LIST         - Select a folder to view
+   A  ADDRESS BOOK        - Update address book
+   S  SETUP               - Configure Alpine Options
+   Q  QUIT                - Leave the Alpine program
+   ```

To read your e-mail, select either I or L. Commands are listed along the bottom of the screen and change to suit the content you are viewing. Left (←) and right (→) arrow keys let you step backward and forward among the alpine screens.

# Mail Reader

The mail command was the first mail reader for UNIX. It is text-based, but not screen-oriented. Type `mail` and you will see the messages in your mailbox. Because mail is not screen-oriented, you just get a prompt after message headings are displayed — you are expected to know what to do next. (You can use the [Enter] key to step through messages.) Type `?` to see which commands are available.

While in mail, type `h` to see mail headings again. Simply type a message number to see the message. Type `d#` (replacing `#` with a message number) to delete a message. To create a new message, type `m`. To respond to a message, type `r#` (replacing `#` with the message number). Type `man mail` to learn more about the `mail` command.