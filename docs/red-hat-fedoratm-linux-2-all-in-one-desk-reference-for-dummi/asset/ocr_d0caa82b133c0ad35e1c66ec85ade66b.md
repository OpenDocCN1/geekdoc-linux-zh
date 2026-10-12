+   2. **Rebuild the** `/etc/mail/sendmail.cf` **file with this command:**
+   
+   `m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`
+   
+   3. **Restart sendmail with the following command:**
+   
+   `service sendmail restart`

# ## sendmail.cf file syntax

The sendmail.cf file’s syntax is designed to be easy to parse by the sendmail program because sendmail reads this file whenever it starts. Human readability was not a primary consideration when the file’s syntax was designed. Still, with a little explanation, you can understand the meaning of the control lines in sendmail.cf.

Each sendmail control line begins with a single-letter operator that defines the meaning of the rest of the line. A line that begins with a space or a tab is considered a continuation of the previous line. Blank lines and lines beginning with a pound sign (#) are comments.

Often, no space is between the single-letter operator and the arguments that follow the operator, which makes the lines even harder to understand. For example, sendmail.cf uses the concept of a class — essentially a collection of phrases. You can define a class named P and add the phrase REDIRECT to that class with the following control line:

```
CPREDIRECT
```

Because everything is jumbled together, the command is hard to decipher. On the other hand, to define a class named Accept and set it to the values OK and RELAY, write the following:

```
C{Accept}OK RELAY
```

This command may be slightly easier to understand because the delimiters (such as the class name, Accept) are enclosed in curly braces.

Other — more recent — control lines are even easier to understand. For example, the line

```
O HelpFile=/etc/mail/helpfile
```

defines the option HelpFile as the filename /etc/mail/helpfile. That file contains help information sendmail uses when it receives a HELP command.

![](bbox=[0.88, 0.72, 0.94, 0.89])