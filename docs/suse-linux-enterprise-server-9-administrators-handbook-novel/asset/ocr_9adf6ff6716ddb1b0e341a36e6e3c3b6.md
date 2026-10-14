```
AD

Login          : caro]
Password       : ***********
DN             :
Rules          :
accept 10.0.17.0/25
default deny

Is that ok ? (Y/n) [y] y
user added.
Athena:~ #
```

Before the server side of Nessus is invoked, you should perform one important step. Vulnerabilities are being discovered on a regular basis. A list of known weaknesses from the original install CDs will most certainly be out of date by the time you install Nessus. Therefore, before you start Nessus as well as on a regular interval, it is important to update the list of known vulnerabilities. This ensures the validity of the scan results. Nessus uses plug-ins for scanning. These plug-ins are brought up to date using the nessus-update-plugins command. At the time of writing, there were more than 7,200 Nessus plug-ins.

After you run the update command, you can start the Nessus server daemon by issuing the following command:

```
Athena:~ # nessusd -D
Loading the plugins... 1224 (out of 7297)
```

After the server has loaded all the plug-ins, the system prompt will return. The client can now be invoked, as follows:

```
Athena:~ # nessus &
```

On startup, the client requires credentials for authenticating against the Nessus scanner on the server side. In addition, if firewalls are in place, allowances for port 1241 will have to be made for client/server communications. The default login screen is shown in Figure 12.1.

The Nessus client interface is composed of a number of tabs. Each tab represents a family of options allowing you to customize your scans. The major tabs are

+   - **Plugins**—This tab allows you to define the series of tests that will be performed on the selected target.
+   - **Credentials**—This tab allows you to define valid application accounts (SMB and ssh) to be used to probe for known vulnerabilities available to authenticated users.