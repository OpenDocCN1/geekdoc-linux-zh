
# USING ELECTRONIC MAIL

6. When you finish editing, save the changes into the file and quit the editor. Do this with the usual commands:

```
(Esc) :wg (Return)
```

This will put you back in the mail program. You may see a prompt of some sort:

```
( continue )
```

7. Send the message. This is done the usual way:

```
(Return)
(Control-D)
```

You may be asked to specify carbon copies.

```
Cc:
```

8. Send the carbon copies, if any. Press `(Return)` if you do not wish to send any copies:

```
Cc: (Return)
```

This will get you out of the mail program and back into the UNIX shell:

```
$
```

## 14.4 Your Mailboxes

The mail program uses two kinds of mailboxes. Your *system mailbox* is a file that holds mail you have received but have not read, deleted, or saved to another file. On many systems, this file is located in the `/var/spool/mail` directory, and has the same name as your user ID. For example, if your user ID is *jdoe*, then your system mailbox is the file `/var/spool/mail/jdoe`.

In addition to the system mailbox, you may have a *personal mailbox*. This is a file named `mbx` in your home directory. Any mail messages you have read but not deleted or saved in another file are automatically put into your `mbx` file when you quit the mail program.

If you use either the Bourne Shell or Korn Shell, your shell checks your system mailbox periodically and notifies you of any new messages:

```
New mail has arrived.
```

You can also use the `biff` or `xbiff` program to alert you when new mail arrives. These programs are discussed in the exercises.

### 14.5 Reading Your Mail

You can read the messages in your system mailbox with the same electronic mail program that you used to send messages:

1. **Start the mail program without specifying a recipient**. How you do this depends on whether your system uses `mail` or `mailx`:

   - `$ mail` `Return`
   - or
   - `$ mailx` `Return`

The mail program will list the messages in your system mailbox:

```
>U 1 yourlogin Thu Nov 22 15:27 11/321 "Test Message"
 N 2 yourlogin Thu Nov 22 15:35 11/321 "Test Message #2"
 N 3 yourlogin Thu Nov 22 15:42 20/442
&
```

The `>` in the first column points to the current message. A `U` indicates a previously unread message; `N` indicates a new message. The messages are numbered (1 through 3 in this case). The login name and address of the sender is shown, along with the date and time the message was received and the number of lines and characters the message contains (lines/characters). The subject of the message is given in quotes.

The ampersand (`&`) on the last line is the *mail prompt*. It tells you that the mail program is awaiting your instructions. Some systems use a question mark (`?`) as a prompt.

2. **If necessary, list the next screenful of messages**. If there are too many messages in your mailbox to list on one screen (perhaps because you have many admirers or have not been keeping up with your mail), you can list the next screenful by typing a `z` at the mail prompt:

   ```
   &z Return
   ```

   You can list the previous screenful of messages again by typing `z-` (`z` hyphen):

   ```
   &z- Return
   ```

   To list the current screenful of messages, enter `h` at the mail prompt:

   ```
   &h Return
   ```

3. **Select a message to read**. To do this, simply type in the message number at the prompt and press `Return`. To see the second message, for example, type

   ```
   &2 Return
   ```

This will cause the second message to appear:

```
Message 2:
From yourlogin Day Month Time Year
Date: Day Month Time Year
From: yourlogin (Your name)
To: (Your login name)
Subject: Test Message #2

Don't be alarmed. This is only a test.
&
```

The mail program places some additional lines at the top of a message before sending it on. These lines make up the *mail header*, which contains such information as the name, the login, and the address of the person who sent the message. Note that the mail header makes it difficult to send an anonymous mail message!

Once you have read the message, there are a number of things you can do with it. Without leaving the mail program, you can reply to the message, save it in a file, or delete it.

## 14.6 Replying to a Message

It is a good idea to respond promptly to any e-mail that you receive. While you are still in the mail program, use the R (“Reply”) command.

1. **Enter the Reply command and specify a message number.** Thus, to reply to the second message, type

   ```
   &R2 (Return)
   ```

   This tells the mail program that you want to reply to the user who sent the second message. The mail program will take care of addressing your reply; it even fills in the Subject field for you.

   ```
   Subject: Re: Test Message #2
   ```

2. **Enter your message.** This is done as you did before:

   ```
   What a relief.
   ```

3. **Send the message.** Press `(Return)`, then `(Control)-D`:

   ```
   (Return)
   (Control)-D
   ```

## 14.7 Saving Messages

You may decide to keep some messages for future reference. You can save a message in a file with the s (“save”) command.

- Enter the **Save** command, followed by the **message number**. Thus, to save the message 1 in a file named `message1.file1`, type

  ```
  &s1 message1.file1 (Return)
  ```

This creates a new file in your home directory named `message1.file1`, and places in it the text of the message, including the mail header. (If you already have a file named `message1.file1` in your home directory, the message is appended to the file.) The original message is deleted from your system mailbox. The mail program will tell you that the message has been saved.

## 14.8 Deleting Messages

Some messages are not worth saving. You should delete these with the d (“delete”) command.

1. Enter the **Delete** command, followed by the **message number**. For example, to delete the third message, type

   ```
   &d3 (Return)
   ```

   Normally, the mail program does not tell you that it has deleted a message. Instead, it will simply show you a mail prompt:

   ```
   &
   ```

2. **Check that the message has been deleted.** The h (“headers”) command will list the messages remaining in the mailbox:

   ```
   &h (Return)
   ```

   A deleted message will no longer appear in the list of mail headers.

## 14.9 Restoring Deleted Messages

What if you delete a message by accident and want to get it back? If you have not exited the mail program, you can retrieve deleted messages using the **Undelete** command.

- Enter the **Undelete** command, followed by the **message number**. For example, to restore the third message, type

  ```
  &u3 (Return)
  ```

## 14.10 Quitting the Mail Program

The x command is useful when you accidentally deleted a message you want to keep.

There are two common ways you can quit the e-mail program after reading your mail, which differ in what is done to the messages in your mailbox. The q ("quit") command puts any messages that you read, but did not delete, into a file named **mbox** in your home directory. Unread messages are left in the system mailbox. The x ("ex-it") command quits the mail program without changing the mailbox, restoring any deleted messages.

Of these, the q command is more commonly used:

- **Type q, then ⏎ (Return):**

  ```
  &q ⏎ (Return)
  ```

  Some versions of the mail program will tell how many messages were saved in the mailbox and how many were placed in your mbox file:

  ```
  Saved 3 messages ...
  ```

## 14.11 Reading Your mbox File

Your **mbox** file receives messages that you have read but not deleted or saved in another file. Using the mail program with the -f ("file") option allows you to read and process the messages in your **mbox** file just as you did with the messages in your system mailbox.

1. **Start the mail program with the -f option.**

   - `$ mail -f ⏎ (Return)`
   - or
   - `$ mailx -f ⏎ (Return)`

   The mail program will list the messages in your **mbox**.

2. **Process the messages.** You can use the usual mail commands to read, reply to, and delete messages.

3. **Quit the mail program.** Either the q or x command will do this.
