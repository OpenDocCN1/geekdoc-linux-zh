entry value is created as null automatically when adding any registry key. We will follow the application protocol specifications and replace the empty (Default) value with an executable of our choice, **cmd.exe**. This should force fodhelper to handle the *ms-settings:* protocol with our own executable!

In order to test this theory, we’ll set our new registry value. We’ll also specify the new registry value with */d* **“cmd.exe”** and */f* to add the value silently.

```
```
C:\Users\admin> REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command /d "cmd.exe" /f
The operation completed successfully.
```
*Listing 562 - Setting the (Default) value to cmd.exe*
```

After setting the value and running **fodhelper.exe** once again, we are presented with a command shell:

![](bbox=[0.12, 0.35, 0.88, 0.71])

The output of the *whoami* */groups* command indicates that this is a high-integrity command shell. Next, we’ll attempt to change the admin password to see if we can successfully bypass UAC:

```
```
C:\Windows\system32> net user admin Ev!lpass
The command completed successfully.
```
*Listing 563 - Successfully changing the password of the admin user after spawning cmd.exe with high integrity via fodhelper.exe*
```

The password change is successful and we have successfully bypassed UAC!

This attack not only demonstrates a terrific UAC bypass, but also reveals a process that we could use to discover similar bypasses.