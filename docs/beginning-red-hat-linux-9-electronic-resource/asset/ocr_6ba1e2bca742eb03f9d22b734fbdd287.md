> *Note that normal accounts that have access to the Samba services also have access to SWAT. However, only root users have access to the full range of SWAT’s utilities; normal users are only allowed to use limited features contained in the HOME, STATUS, VIEW, and PASSWORD screens.*

# ## Creating and Configuring a Samba Share

Now we’re ready to configure our Linux server as a file server, by creating a **share** (a dedicated directory on the server that will be accessible to other users). We can do all this using SWAT:

+   1. Create a directory, which we’ll call `/share`, to be used for the file server. With root permission, you can do this at the command line using this command:

```
# mkdir /share
```

+   2. If you haven’t done so already, use the Mozilla browser (or your favorite web browser) to browse to the SWAT home page at `http://localhost:901`, and log in using the root user account.

+   3. Click on the **GLOBALS** toolbar icon. In the **Base Options** section, use the **Workgroup** field to enter the name of the workgroup that you want your server to appear in when clients use it. (If you haven’t set up a workgroup, then this is probably the default value, **WORKGROUP**). You should also name the service, by entering a value in the **server string** field – it can be any string that you want your Samba clients to see. We’ll stick with the default, **Samba Server**:

![](bbox=[0.14, 0.55, 0.87, 0.92])