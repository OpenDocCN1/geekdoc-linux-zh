$creds = Get-Credential

# connect to vCenter
Connect-VIServer -hostname -Credential $creds

Get-Credential cmdlet opens a dialog box, shown in Figure 25.4, prompts for a username and password. These are stored securely so they cannot be seen by others using the system. The downside to this implementation is that someone must be interactively using the system—you cannot use this method for scheduling a script to run unattended.

# FIGURE 25.4 Prompting for credentials

![](bbox=[0.458, 0.326, 0.722, 0.503])

# Store the Password Securely and Retrieve when Needed

This is, by far, the best method to use for storing credentials for scripts that will be executed via a scheduled task. The password is always in a secure format, preventing eyes from attempting to gain privileges they shouldn't have. To enhance security, the Windows Data Protection APIs used by the credential management cmdlets prevent a user other than the original creator from accessing the stored values.

The first step is to collect the credentials. This has to be done once for each unique username and password combination. After the username and password are stored in a variable, you convert the password to a secure string object and write it to a file for later usage.

```
# collect credentials and store them in a variable
$creds = Get-Credential
```

```
# convert the password to a secure string
$password = $creds.Password | ConvertFrom-SecureString
```