unencrypted connections. Using Gmail as an example, you can create an SSL connection with the following code.

```
import imaplib
import getpass
my_imap = imaplib.IMAP4_SSL('imap.gmail.com')
```

As opposed to poplib, imaplib has a single method to handle authentication. You can use the getpass module to ask for the password.

```
my_imap.login('my_username@gmail.com',
getpass.getpass())
```

IMAP contains the concept of a tree of mailboxes where all of your emails are organised. Before you can start to look at the emails, you need to select which mailbox you want to work with. If you don't give a mailbox name, the default is the inbox. This is fine since we only want to display the newest emails which have come in. Most of the interaction methods return a tuple that contains a status flag (either 'OK' or 'NO') and a list containing the actual data. The first thing that we need to do after selecting the inbox is to search for all of the messages available, as shown in the following example.

```
my_imap.select()
typ, email_list = my_imap.search(None,
'ALL')
```

The email_list variable contains a list of binary strings that you can use to fetch individual messages. You should check the value stored in the variable typ to be sure that it contains 'OK'. To loop through the list and select a particular email you can use the following code:

```
for num in email_list[0].split():
    typ, email_raw = my_imap.fetch(num, '(RFC822')
```

The variable email_raw contains the entire email body as a single escaped string. While you could parse it to pull out the pieces that you want to display in your email monitor, that kind of defeats the power of Python. Again, available in the standard library is a module called email that can handle all of those parsing issues. You will need to import the module in order to use it, as in the example here.

```
import email
email_msg = email.message_from_bytes(email_raw[0][1])
```

All of the sections of your email are now broken down into sections that you can pull out much more easily. Again, to pull out the subject line for a quick display, you can use the code:

```
subject_line = email_msg.
get('Subject')
```

There are many different potential items that you can select out. To get the full list of available header items, you can use the keys method, as below:

```
email_msg.keys()
```

Many times, the emails you get will come as multi-part messages. In these cases, you'll need to use the get_payload() method to extract any attached parts. It will come back as a list of further email objects. You then need to use the get_payload() method on these returned email objects to get the main body. The code might look like:

```
payload1 = email_msg.get_payload()[0]
body1 = payload1.get_payload()
```

As with POP email connections, you may need to do something to keep the connection from timing out. If you do, you can use the noop() method of the IMAP connection object. This method acts as a keep-alive function. When you are all done, you need to be sure to clean up after yourself before shutting down. The correct way to do this is to close the mailbox you have been using first, and then log out of the server. An example is given here:

```
my_imap.logout()
my_imap.close()
```

You now should have enough information to be able to connect to an email server, get a list of messages, and then pull out the sections that you might want to display as part of your email monitor. For example, if you are displaying the information on an LCD, you might just want to use the subject lines scrolling past. If you are using a larger screen display, you might want to grab a section of the body, or the date and time, to include as part of the information.

# ## What about sending emails?

In the main article, we have only looked at how to connect to an email server and how to read from it. But, what if you'd like to be able to also send emails using code? Similar to poplib and imaplib, the Python standard library includes a module called smtplib. Again, similar to poplib and imaplib, you need to create an SMTP object for the connection, and then log in to the server. If you're using the Gmail SMTP server, you could use the code:

```
import smtplib
import getpass
my_smtp = smtplib.SMTP_SSL('smtp.gmail.com')
my_smtp.login('my_email@gmail.com', getpass.getpass())
```

This code asks the end user for their password, but if you aren't concerned about security, you could have it hard-coded into the code. Also, you only need to use the login() method for those servers that require it. If you're running your own SMTP server, you may have it set up to accept unauthenticated connections. Once you're connected and authenticated, you can now send emails out. The main method to do this is called sendmail(). As an example, the following code sends 'Hello World' email to a couple of people:

```
my_smtp.sendmail('my_email@gmail.com', ['friend1@email.com',
'friend2@email.com'],
'This email\r\nSans\r\nHello World')
```

The first parameter is the 'from' email address. The second parameter is a list of 'to' email addresses. If you only have one 'to' address, you can still use a single string rather than a list. The last parameter is a string containing the body of the email. One thing to be aware of is that you will only get an exception if the email can't be sent to any of the 'to' email addresses. As long as the message can be sent to at least one of the addresses, it will return as completed. Once you have finished sending your emails, you can clean up with the code:

```
my_smtp.quit()
```

This cleans everything up and shuts down all active connections. So now your project can reply to incoming emails, too.