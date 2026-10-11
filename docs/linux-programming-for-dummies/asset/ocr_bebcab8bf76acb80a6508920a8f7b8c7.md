Type the logout command and then press the Enter key to log out of the user ID, as follows:

```
logout
```

After you log out, you again find yourself at the command prompt.

You can log in as root by typing the following and then pressing the Enter key:

```
login root
```

Linux prompts you to enter the root password. Do so and press the Enter key. Linux changes the prompt to the following:

```
root@mycomputer
```

# Using the Mail Utility

The mail utility is a tool available in Linux to automatically process outgoing and incoming e-mails. All you need to do is provide the mail utility with specific information and sit back, knowing that the electronic postal carrier is handling your message.

The mail utility performs the following tasks:

+   - Receives e-mail someone sends to a user’s e-mail address.
+   - Displays incoming e-mail on-screen.
+   - Creates e-mails.
+   - Sends e-mails.

You have two mailboxes: an *incoming box*, where you receive e-mail for a user ID, and an *outgoing mailbox*, where the utility keeps e-mails that the user ID sends out for transmission. The mail utility uses the user IDs to identify the user mailboxes.

# Creating e-mail

Although you can use the mail utility to create an e-mail, I find that using a text editor such as vi to create my e-mail is more efficient.

To use vi to create an e-mail, type the following at the command line and press the Enter key:

```
vi mesol
```