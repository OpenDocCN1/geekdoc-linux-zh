Windows defines the executable to launch when a particular URL is used by a program. These URL-Application mappings can be defined through Registry entries similar to the ms-setting key we found in HKCR (Figure 286 above). In this particular case, the application protocol schema for ms-settings passes the execution to a COM$^{521}$ object rather than a program. This can be done by setting the `DelegateExecute` key value$^{522}$ to a specific COM class ID as detailed in the MSDN documentation.

This is definitely interesting because fodhelper tries to access the ms-setting registry key within the HKCU hive first. Previous results from Process Monitor clearly showed that this key does not exist in HKCU, but we should have the necessary permissions to create it. This could allow us to hijack the execution through a properly formatted protocol handler. Let's try to add this key with the `REG`$^{523}$ utility:

```
```
C:\Users\admin> REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command
The operation completed successfully.

C:\Users\admin>
```
```

Once we have added the registry key, we will clear all the results from Process Monitor (using the icon highlighted in Figure 287), restart `fodhelper.exe`, and monitor the process activity:

![](bbox=[0.11, 0.44, 0.88, 0.74])

Please note that clearing the output display does NOT clear the filters we created. They are saved and we do not need to recreate them.