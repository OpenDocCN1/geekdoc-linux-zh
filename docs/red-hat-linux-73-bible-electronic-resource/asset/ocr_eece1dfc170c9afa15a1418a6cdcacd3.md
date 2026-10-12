# Pine mail reader

> **NOTE:** To use the `pine` mail reader you must have the `pine` software package installed.

The `pine` mail reader is another full-screen mail reader, but it offers many more features than does `mutt`. With `pine`, you can manage multiple mail folders. You can also manage newsgroup messages, as well as mail messages. As text-based applications go, `pine` is quite easy to use. It was developed by a group at the University of Washington for use by students on campus, but has become widely used in UNIX and Linux environments.

Start this mail program by typing `pine`. The following menu is displayed, from which you can make a selection by typing the associated letter or using up and down arrows and pressing Enter:

```
```
? HELP              - Get help using Pine
C COMPOSE MESSAGE   - Compose and send a message
I MESSAGE INDEX     - View messages in current folder
L FOLDER LIST       - Select a folder to view
A ADDRESS BOOK      - Update address book
S SETUP             - Configure Pine Options
Q QUIT              - Leave the Pine program
```
```

To read your e-mail, select either I or L. Commands are listed along the bottom of the screen and change to suit the content you are viewing. Left (←) and right (→) arrow keys let you step backward and forward among the `pine` screens.

# Elm mail reader

This is yet another text-based and form-based mail reader. When you first start `elm`, it sets up several mail directories and files in your home directory. Then it opens a very basic interface to your incoming mailbox (as set by the `$MAIL` variable).

On the Mailbox screen, `elm` identifies your mailbox and shows the headings for the first page of mail messages. Move up and down among the messages with arrow keys (or with `j` and `k` keys, as in the `vi` editor). Press Enter to open the current mail message and press `i` to return to the index. Other commands are shown at the bottom of the screen.

# Mail reader

The `mail` command was the first mail reader for UNIX. It is text-based, but not screen-oriented. Type `mail` and you will see the messages in your mailbox. Because `mail` is not screen-oriented, you just get a prompt after message headings are displayed — you are expected to know what to do next. (You can use arrow keys to step through messages.) Type ? to see which commands are available.

While in `mail`, type `h` to see mail headings again. Simply type a message number to see the message. Type `d#` (replacing `#` with a message number) to delete a message. To create a new message, type `m`. To respond to a message, type `r#` (replacing `#` with the message number.