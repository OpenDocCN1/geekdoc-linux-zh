were a global configuration, we'd save the file as **/etc/dt/appconfig/appmanager/instinfo**.

+   5. Change the permissions to include execute as follows:
+   
+   `chmod 555 $HOME/.dt/appmanager/instinfo`
+   
+   Now it's time to modify the front panel to include the icon and action we just created. The front panel file, **dtwm.fp**, is located in the **/usr/dt/app-config/types/C** directory. Because we don't want to overwrite the system file, we need to copy it locally and then modify it for our use.
+   
+   1. Copy this to **/$HOME/.dt/types/dtwm.fp** for AIX and HP-UX and to **/$HOME/.dt/types/fp-dynamic/dtwm.fp** for Solaris. For the admin user, that would be:
+   `cp /usr/dt/appconfig/types/C/dtwm.fp /home/admin1/.dt/types/fp-dynamic/dtwm.fp`
+   
+   or for Solaris:
+   `cp /usr/dt/appconfig/types/C/dtwm.fp /home/admin1/.dt/types/fp-dynamic/dtwm.fp`
+   
+   2. **Using your favorite editor**, modify the local **dtwm.fp** file.
+   
+   As we look at the file, we notice that it is in the same order as the front panel is displayed. The clock is the first CONTROL in the file and the first item on the front panel. Also notice that the POSITION_HINTS is 1. Date is next and so is POSITION_HINTS 2. What we want to do is put our new icon and action after POSITION_HINTS 4, the TextEditor CONTROL.
+   
+   3. Go down just past the ] ending CONTROL TextEditor and before CONTROL Mail. At this point, **insert the following exactly as shown below**. Make sure that the uppercase letters are capitalized and the lowercase letters aren't.

```
CONTROL Info
{
    TYPE            icon
    CONTAINER_NAME  Top
    CONTAINER_TYPE  BOX
```