
### Session Timeout
Specify the maximum length of time (in minutes) that a session will be continued when there is no synchronization activity.
If the session times out, the client must go through a reconnect step before its next synchronization.

### Debug Output
Select the check box to enable synchronization activity to be logged and available for analysis.

When you finish, select **Update**.

## Use Debug Output

To use Debug Output for Linux servers, do the following:

1. Create a logs folder in `/var/opt/novell/ifolder/DocumentRoot/`.
2. Edit the `httpd_ifolder_unix.conf` file located at `/etc/opt/novell/ifolder`, and add the following parameter to the end of the file:

```
iFolderServerLogging " "/var/opt/novell/ifolder/DocumentRoot/logs/index.html"
```

The debug information will go to the `index.html` file that is created for you in `DocumentRoot` under the `logs` directory.

3. Give Apache permissions to create and write to the log file by entering the following at the shell prompt:

```
chmod 757 /var/opt/novell/ifolder/DocumentRoot/logs
```

4. Restart the iFolder service so your changes to the conf file will take effect by entering the following:

```
/etc/init.d/novell-httpd stop
/etc/init.d/novell-httpd start
```

5. To access this information, do one of the following:
   - In a browser on a workstation, enter the following:
     **http://iFolder DNS or IP address/iFolder/logs/index.html**
     For example:
     `http://DA3.DigitalAirlines.com/iFolder/logs/index.html`
   - In a Linux browser on the iFolder server, enter the following:
     **/var/opt/novell/ifolder/DocumentRoot/logs/index.html**
   - At a shell prompt on the Linux iFolder server, enter the following:
     **tail -f /var/opt/novell/ifolder/DocumentRoot/logs/index.html**

## How to Manage LDAP Servers

Whenever you add an LDAP server through the iFolder Management console for user authentication, you are required to enter a name for the LDAP server, its DNS or IP address, a port number and, if necessary, the location of the root certificate.

You can have up to eight LDAP servers.

To manage LDAP servers for iFolder, you need to know how to do the following:

- Choose Port 389
- Choose Port 636
- Add LDAP Contexts

### Choose Port 389

Choose port 389 if you want to use LDAP without SSL encryption or if your LDAP server does not support SSL.

Port 389 is also a good choice if iFolder and LDAP are running on the same server (no communication or data is being transferred across the wire, so no encryption is necessary).

If you choose port 389, the LDAP Group object must be configured to allow clear text passwords.

### Choose Port 636

Choose port 636 if you want to use SSL to provide your network with encryption and security when data is transferred across the wire. SSL requires a root certificate.

If you choose port 636, make sure you have previously copied the `rootcert.der` file to the appropriate location on your system.

When you add a secure LDAP server to your iFolder system, the root certificate is copied into an attribute of the `iFolderSettings` class on the Global Settings LDAP.

### Add LDAP Contexts

In the **Contexts** field, list all of the contexts, separated by semicolons (`;`) with no spaces.

The order of the contexts is the order in which the contexts will be searched. The first context that is listed should be the context that contains the Admin user.

## How to Monitor Your iFolder System

To monitor your iFolder system, go to the iFolder Management console; then click **System Monitoring**.

The following appears:

Figure 6-13

![](img/d63035f3fce0eaaf97203dde900affb7_66_0.png)

This section of the iFolder Management console lists the following:

- **Each User LDAP server.** For each server, iFolder lists the IP address, the status, the number of LDAP users, and the number of iFolder users.
- **Each iFolder Server.** For each server, iFolder lists the IP or DNS name, status, number of user accounts, current users, current sessions, available disk space, and the amount of time the server has been up and running.
- **Stop Sync.** This option stops synchronization on a selected iFolder server.

## How to Generate Reports

Novell iFolder provides a report generator that lets you observe and assess information in the following categories:

**Table 6-2**

| General Info | iFolder Servers | User LDAPs | User Accounts |
| :--- | :--- | :--- | :--- |
| Total Number of Users | iFolder Server Name | LDAP Name | Username |
| Total Disk Quota | IP Address or DNS Name | IP Address or DNS Name | iFolder Server Name |
| Total Disk Space Used | Server Up Time | Status | Used Space |
| | iFolder Server Version | LDAP Users | Quota |
| | User Accounts | iFolder Users | Last Sync |
| | Current Users | | Files |
| | Current Sessions | | Directories |
| | Total Disk Space Used | | Upload |
| | Total Disk Quota | | Download |
| | iFolder Host OS | | Encryption |
| | iFolder Host Web Server | | |
| | User Data | | |
| | Application Root | | |

To run reports on your iFolder system:

1. Go to the iFolder Management console; then select **Reporting**.
2. Select **General Info**, **iFolder Servers**, **User LDAPs**, or **User Accounts**.
3. Select **Export**.

A report such as the following iFolder User Accounts report appears:

Figure 6-14

![](img/d63035f3fce0eaaf97203dde900affb7_68_0.png)

4. Save the displayed data to your hard drive in HTML format.
5. Import the data from 1 or more iFolder report files to another application such as **OpenOffice Writer**.
6. Create statistics, graphs, and reports to suit your management needs.

## Exercise 6-2 Configure and Test iFolder

**45 minutes**

Organize students to do Part II one at a time on the workstation. This part of the exercise cannot be done on the NNLS server.

The first student to do Part II will install the client and use it to log in as an iFolder user. The second student will only be able to log in as one of his or her iFolder users.

In this exercise, you do the following:

- Part I: Configure iFolder for Employee Access
- Part II: Install and Use the iFolder Client
- Part III: Configure iFolder to Log Debug Information
- Part IV: Change and Test the iFolder Configuration

### Part I: Configure iFolder for Employee Access

Do the following:

1. Configure the user context for your office employees:
    - a. From your NNLS server desktop, launch **Mozilla**; then enter the following:
      `https://DAx.your container.DigitalAirlines.com/iFolderServer/Admin`
    - b. Select **Global Settings**.
    - c. Log in as username **admin**, with the password **novell**.
    - d. At the left under **Global Settings**, select **User LDAPs**.
    - e. At the right, select **iFolder_ldap01**.
      A properties page for **iFolder_ldap01** appears. Under **Contexts To Search**, you see the context listed for your container.
    - f. Enable the context by selecting the **check box** to the left of **o=your container**.
    - g. Enable subcontainer search by selecting the **Search Subcontexts?** check box.
    - h. When you finish, select **Update**.

The check mark in the box to the left disappears, indicating that the update was successful.

2. Enable your office employees to access iFolder:
    - a. Select the **User Management** icon at the top of the page.
    - b. At the left under **User Management**, select **Search**.
      A **Search for User** page appears.
      You are using the Search feature in this exercise because you only have a small number of employees to enable.
      However, if you have many users you need to enable, use Advanced Search to find, select, and enable several users at the same time.
    - c. Enable the following employees:
        - [ ] **cgrayson**
        - [ ] **ddecker**
        - [ ] **jjackson**
      Do the following:
        - a. Enter the first initial of the username in the search field (i.e., for cgrayson, enter c); then select **Search**.
          A list of names appears.
        - b. Select the first of the above *employees*; then, from the drop-down list, select **iFolder_server01**.
        - c. Select **Enable**.
          The page is re-displayed with a Disk Quota of 200 MB for the user. A message also indicates that the account has not been activated by the user.
        - d. Repeat these steps to enable the two other employees.
          You have finished enabling your employees.

3. Log out of the iFolder Management console.

Students might notice that some of the employees in the list are already iFolder enabled (yellow with the red letter i). Note that the difference is that objects that were imported in the LDIF are not already enabled and the users created in class are already enabled.
