5. List the names of the three protocols that enable email to be delivered.

# # Programming Assignment

# ## Exercise 1: Perform Domain-Name Resolution

Using the nslookup command, list the IP addresses of six Web sites.

# ## Exercise 2: Send Manual Email

In this exercise, you'll use the telnet utility to connect to an email server and send someone an email. To complete this exercise you'll need the following:

+   * The domain name of an email server
* A sender email address
* A receiver email address (which can be the same as the sender, if need be)

+   1. Telnet to an email server, replacing servername in the following with your actual email server:

```
$ telnet smtp.servername.net 25
```

You should get a 220 response message if all went well

+   2. Identify yourself, replacing username with your actual user name:

```
HELO username
```

+   3. Say who the mail is from, replacing me@myisp.net in the following with your email address:

```
mail from: me@myisp.net
```

You should get a 250 message saying "Sender ok."

+   4. Say who the email is sent to, replacing you@yourisp.net with the receiver's email address:

```
rcpt to: you@yourisp.net
```

You should get a 250 message saying "Recipient ok."

+   5. Enter the data command. You should get the following 354 message:

```
Enter mail
```