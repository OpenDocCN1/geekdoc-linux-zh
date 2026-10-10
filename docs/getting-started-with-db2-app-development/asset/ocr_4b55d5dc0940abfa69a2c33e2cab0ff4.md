![](bbox=[0.15, 0.16, 0.76, 0.38])

**Figure 7.9 - Creating the RoR application myapp1**

+   3. Change the work directory to <app_home>, the directory for your application:

```
cd myapp1
```

+   4. Start the WEBrick Web Server:

```
ruby script/server
```

When the Web server starts, it will report the process ID (PID) and TCP/IP listening port number which should default to 3000. This is illustrated in Figure 7.10.

![](bbox=[0.15, 0.54, 0.84, 0.7])

**Figure 7.10 - Starting the WEBrick Web Server**

Now that the Web server is up and running, open a browser and redirect it to http://localhost:3000/ which will take you the Welcome page shown in Figure 7.11.