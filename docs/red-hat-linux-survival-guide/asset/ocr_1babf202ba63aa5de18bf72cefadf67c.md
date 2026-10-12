will use the your_username and your_password as the password to log you in. The macdef init line defines an initialization macro, which is simply a list of commands that you want the client program to perform automatically. Here the first command is bin, which sets the binary transfer mode; the next command toggles the prompt mode; the cd /some/path command changes the path on the FTP server and then uses the get filename command to download a file and finally uses the quit command to terminate the connection.

![](bbox=[0.07, 0.31, 0.15, 0.38])

> Notice that there are two blank lines after the last command (quit); these indicate that this macro ends there.

You can add multiple machine records to automate FTP upload or download for commonly used FTP servers.

![](bbox=[0.07, 0.46, 0.15, 0.54])

> You must set the .netrc file permission to be 600 so that only the file owner can read or write the file. You can run chmod 600 ~/.netrc command to set this permission.

Although the above-mentioned permission setting ensures that no one but the owner can read the .netrc file, you may wish to remove the password line if you do not wish to save your password in a text file only protected via a permission setting. This way you can still use the automation that .netrc provides, with the exception that you will be prompted for the password once.

When the FTP client can't find a matching machine record for the FTP server you are trying to connect, it looks for a default setting to be used. For example, you can add the following line as the very last line in your .netrc file:

```
default login anonymous password your@email_address
```

Now whenever you try to connect to an FTP site that does not have a machine record in .netrc, it will use the default login (anonymous).

![](bbox=[0.07, 0.88, 0.15, 0.95])

> This may not be desirable if you connect to many non-anonymous FTP sites and do not wish to add them in your .netrc file.