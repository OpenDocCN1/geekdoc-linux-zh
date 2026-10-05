
# OffSec

## Penetration Testing with Kali Linux

```powers
PS C:\Users\dave Get-ChildItem -Path C:\xampp -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue
Get-ChildItem -Path C:\xampp -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue
Directory: C:\xampp\mysql\bin
```

| Mode | LastWriteTime | Name |
| --- | --- | --- |
| -a---- | 6/16/2022 1:42 PM | 5786 my.ini |
| -a---- | 3/13/2017 4:04 AM | 824 passwords.txt |
| -a---- | 6/16/2022 10:22 AM | 792 properties.ini |
| -a---- | 5/16/2022 12:21 AM | 7498 readme_de.txt |
| -a---- | 5/16/2022 12:21 AM | 7368 readme_en.txt |
| -a---- | 6/16/2022 1:17 PM | 1200 xampp-control.ini |

Listing 389 shows that our search found two files that contain sensitive information. The file my.ini is the configuration file for MySQL and passwords.txt contains the default passwords for the XAMPP components. Review them.

```powershell
PS C:\Users\dave type C:\xampp\passwords.txt
type C:\xampp\passwords.txt
### XAMPP Default Passwords ###

1) MySQL (phpMyAdmin):

User: root
Password: 
(means no password!)
...
Postmaster: Postmaster (postmaster@localhost)
Administrator: Admin (admin@localhost)

User: newer
Password: wamp
...
PS C:\Users\dave type C:\xampp\mysql\bin\my.ini
type C:\xampp\mysql\bin\my.ini
type : Access to the path 'C:\xampp\mysql\bin\my.ini' is denied.
At line:1
+ type C:\xampp\mysql\bin\my.ini

+ CategoryInfo : PermissionDenied: (C:\xampp\mysql\bin\my.ini:String)
[Get-Content], UnauthorizedAccessException
+ FullyQualifiedError :
GetContentReaderUnauthorizedError.Microsoft.PowerShell.Commands.GetContentCommandException
```

> 76 (Apache Foundation, 2022), https://www.apache.org/docs/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

Listing 390 - Review the contents of passwords.txt and my.ini

Unfortunately, the C:\xampp\passwords.txt only contains the unmodified default passwords of XAMPP, we don't have permissions to view the contents of C:\xampp\mysql\bin\my.ini.

Next, let's search for documents and files in the home directory of the user dave. We enter *.txt*.pdf*.xls*.xlsx*.doc as extensions to search for and -Path to the home directory.

```powershell
PS C:\Users\dave> Get-ChildItem -Path C:\Users\dave\ -Include \
*.txt*.pdf*.xls*.xlsx*.doc,.docx -File -Recurse -ErrorAction SilentlyContinue
Get-ChildItem -Path C:\Users\dave\ -Include *.txt*.pdf*.xls*.xlsx*.doc,.docx \
File -Recurse -ErrorAction SilentlyContinue
```

| Mode | LastWriteTime | Length | Name |
|------|---------------|--------|------|
| -a- | 6/16/2022 11:28 AM | 339 | asdf.txt |

Listing 391 - Search for files and password manager databases in the home directory of dave

Listing 391 shows we found a file on the desktop of dave named asdf.txt. Let's check the contents of this file.

```powershell
PS C:\Users\dave cat Desktop\asdf.txt
cat Desktop\asdf.txt
notes from meeting:
```

- Contractors won't delete the web app on time
- Login will be done via local user credentials
- I need to install XAMPP and a password manager on my machine
- When beta is deployed on my local pc:
- Steve (the guy with light) gives us his password for testing
password is: securityIsNotOption++++

Listing 392 - Contents of asdf.txt

> That we used instead of type to display the contents of a file in the previous listing. In fact, both commands are aliases for the Get-Content Cmdlet in PowerShell and we can use them interchangeably.

Listing 392 shows that the file we used was for meeting notes. The note states that the web uses local user's credentials and for testing "Steve's password securityIsNotOption++++" can be used.

763 (XAMPP, 2022), https://www.apachefriends.org/faq/windows.html

764 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/powershell.management/get-content?view=powershell-7.2

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

Very nice!

The information gathered in the situational awareness process comes in handy now since we already know that a user named steve exists on the target system. Before we attempt to leverage the password, let's check what groups steve is a member of. For this time, we use the command net user with the username steve to obtain this information.

```powershell
PS C:\Users\dave> net user steve
User name               steve
Last logon              6/16/2022 03:52 PM
Logon hours allowed      All
Local Group Memberships  Remote Desktop Users
Remote Management
```

Listing 393 - Local groups steve is a member of

While the output of net user shows that steve is not a member of the group Administrators, the user is a member of the group Remote Desktop Users. Let's connect to CLIENTWK with RDP and open PowerShell.

![](img/336d6ea891e7464f18ad64426619ced4_487_0.png)
Figure 27. RDP Connection

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

Due to access as new user, and therefore different permissions on files on the system, the process of searching for sensitive information begins again. This is a great opportunity to zoom out here for a moment. This is not true for this specific case, but also for nearly all areas of penetration test. The cyclical nature of penetration test is an important concept for us to grasp because it provides a mindset of continuously reevaluating and including new information in order to freely identify attack vectors. In our search as dave we received a permission error on C:\xampp\mysql\bin\my.ini. Let begin check if we have access to.

```ini
PS C:\Users\steve type C:\xampp\mysql\bin\my.ini
# Example config file for small systems.
# The following options will be passed to all clients
[client]
password for backupadmin
password = admin123admin123!
port=3306
socket="C:\xampp\mysql.sock"
```

Listing 394 - Contents of my.ini

Listing 394 shows that we can access my.ini. The file contains the manually set password admin123admin123!. Additionally, a comment states that this is also the password for backupadmin. Let's review the groups backupadmin is a member of to find out if we can use services as RDP or WinRM to connect to this system as this user.

```powershell
PS C:\Users\steve> net user backupadmin
Local Group Memberships *Administrators
Global Group memberships *Users
The command completed successfully.
```

Listing 395 - Local groups backupadmin is member of

Unfortunately, backupadmin is not a member of the group Remote Desktop Users or Remote Management Users. This means we need to find another way to access the system or execute commands as backupadmin. Since we have access to a GUI we can use Runas which allows us to run a program as a different user. Runas can be used with local or domain accounts as the user has the ability to login to the system. Without access to a GUI we cannot use Runas since the password prompt doesn't accept our input in commonly used shells, such as bash shell or WinRM.

765 (Wikipedia, 2021), https://en.wikipedia.org/wiki/Runas

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

We can use a few methods to access the system as user when certain requirements are met. We can use WinRM or RDP to access the system if the user is a member of the corresponding groups. Alternatively, if the target user has the Log on as a batch job right, we can schedule a task to execute a program of this user. Furthermore, if the target user has an active session, we can use PsExec from Sysinternals.

Since we have access to a GUI, we use Runas in PowerShell to start cmd as backupadmin. We will enter the username as /user/ and the command we want to execute. Once we execute the command, password prompt appears which we'll enter the previously found password.

```powershell
PS C:\Users\steve> runas /user:backupadmin cmd
Enter password for backupadmin:
Attempting to start cmd as user "CLIENTWK\backupadmin" ...
PC:\Users\steve>
```

Listing 396 - Runas to execute cmd as user as backupadmin

Once the password is entered, a new command window appears. The title of the new window starts *running as CLIENTWK*. Let's use whoami to confirm the command line is working and we are indeed backupadmin.

![](img/336d6ea891e7464f18ad64426619ced4_489_0.png)
Figure 238: Cmd running in the context of backupadmin

Figure 238 shows that we are executing commands as user backupadmin.
