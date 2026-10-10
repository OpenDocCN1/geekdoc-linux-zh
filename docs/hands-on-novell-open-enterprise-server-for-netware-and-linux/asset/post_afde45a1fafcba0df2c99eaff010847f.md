
## iFolder Server Configuration

Administrators can use the Server Policies window shown in Figure 10-9 to limit space for each user and to change the default session timeout value.

![](img/840007e8f98ea6653e5877e945c27dc6_429_0.png)

![](img/840007e8f98ea6653e5877e945c27dc6_429_1.png)

![](img/840007e8f98ea6653e5877e945c27dc6_429_2.png)

Clicking the Admin Names link displays the window shown in Figure 10-10, where you specify iFolder administrative user names. The users listed in the Admin Names text box can use the iFolder Management utility to configure iFolder settings. Multiple user names are separated by semicolons. All user names entered must exist in the context shown in the General Information window. In the example in Figure 10-10, all user names must exist in the UAS Organization. To add a user, place a semicolon at the end of the last admin user name followed by the new user's login name. Click the Update button to apply your change.

![](img/840007e8f98ea6653e5877e945c27dc6_430_0.png)

Clicking the User LDAPs link displays a window where you tell the LDAP server which contexts to use when searching for iFolder user names. Before enabling iFolder user accounts, you need to use these steps to set the LDAP context for users:

1. Click the User LDAPs link to display the LDAP iFolder servers (see Figure 10-11).

![](img/840007e8f98ea6653e5877e945c27dc6_430_1.png)

2. Click the iFolder_ldap01 link to display the configuration window in Figure 10-12.

![](img/840007e8f98ea6653e5877e945c27dc6_431_0.png)

Figure 10-12 The iFolder_ldap01 settings window

3. To search the default context, click the check box in the Contexts To Search column. To find users in any subcontainers, click to select the Search Subcontexts check box. To add a new context, click the Add button and then click Search to display a list of contexts (see Figure 10-13). Click a context and then click Add to include it in the contexts to search. In Activity 10-2, you use iFolder Global Settings to add the IT OU to iFolder contexts.

![](img/840007e8f98ea6653e5877e945c27dc6_431_1.png)

Figure 10-13 The Search for context to add window

4. After modifying the User LDAP contexts, click the Update button to apply your changes.

You can click the iFolder Servers link to add iFolder servers to your eDirectory tree. If your iFolder server is overloaded, you might want to install iFolder on another server and then use this option to add the new iFolder server to your eDirectory tree. With this option, administrators can add and configure iFolder servers and assign users to different iFolder servers for better performance.

## Activity 10-2: Viewing and Modifying iFolder Global Settings

**Time Required:** 10 minutes

**Objective:** Use the iFolder Management utility to access configuration information.

**Requirements:** Completion of Activity 10-1 or iFolder installed on the classroom server and Internet Explorer on a Windows XP computer or Java-enabled Firefox on a SUSE Linux 10 computer.

> If you're using iFolder from the classroom server, you need access to an iFolder administrative user account and password. If you don't have access to an administrative user account, your instructor might perform this activity as a class demonstration.

**Description:** In this activity, you use the iFolder Management console to document your iFolder configuration settings and add the IT OU to the iFolder search contexts.

1. If necessary, start your computer, and log on to your local computer.
2. Start your Web browser, and then start iFolder Management by entering the URL `https://IPaddress/iFolderServer/Admin` (replacing *IPaddress* with the IP address of your NetWare 6.5 OES server) to display the Novell iFolder menu options.
3. Click the **Global Settings** icon, and then enter your assigned iFolder user name and password to display the General Information window. (If you're using a dedicated server, enter your administrative user name and password.)
4. Record your default port and context:  
   _______________________________
5. Click the **Global Policies** link, and then click the **Client Policies Display** button. Record the default setting for Sync To Server Delay (sec):  
   _______________________________
6. Click your browser's **Back** button, click the **Server Policies Display** button, and enter **30** in the Session Timeout text box.
7. Click the **Update** button to apply your changes.
8. Click the **Admin Names** link, and record the iFolder administrators:  
   _______________________________
9. Click the **User LDAPs** link, and follow these steps to add the IT OU to the Contexts To Search list:
    - a. Click the *iFolder_ldap01* link to display the contexts to search (shown previously in Figure 10-12).
    - b. Click the **Add** button in the Contexts To Search row to display the Search for context to add window.
    - c. Enter **IT\*** in the Context Name text box, and then click the **Search** button to display a search results window showing your IT context.
    - d. Click the *IT.UAS* container, and then click the **Add** button to add the IT OU to the Contexts To Search list. (If you're using a classroom server, click *IT.#\#UAS* in the search results window, replacing *#\#* with your assigned student number.)
    - e. Click to select the check box next to the ITUAS context, and then click the **Update** button to apply your changes.
    - f. Click the **Home** button to return to the Novell iFolder main window.
10. You can leave the iFolder Management window open for the next activity. If you have finished your session, click the **Exit** button and then close your Web browser.

## Enable User Accounts with User Management

Before users can start using iFolder, their user accounts must be enabled to create a storage area for them in the iFolder directory structure. You can enable users individually or through search options available under the **User Management** heading in iFolder Management. Clicking the **Search** link displays a window where you enter a user name and click the **Search** button (see Figure 10-14). This option is useful when you're adding a single user and already know the user name.

![](img/840007e8f98ea6653e5877e945c27dc6_433_0.png)

**Figure 10-14** Searching for a user

Clicking the **Advanced Search** link displays a window (see Figure 10-15) where you can enter search criteria, such as a portion of a user name, the context, or even the entire server.

![](img/840007e8f98ea6653e5877e945c27dc6_433_1.png)

**Figure 10-15** User Management: Advanced Search window

Clicking the **Search** button starts the search process and displays all user accounts matching the search criteria, as shown in Figure 10-16. After the users are listed, you can use the **Enable** and **Disable** buttons to enable or disable just the user names you have selected or to enable or disable all users in the search field. In the following activity, you enable all users in your IT Department to use iFolder.

![](img/840007e8f98ea6653e5877e945c27dc6_434_0.png)

Figure 10-16 Viewing search results

### Activity 10-3: Enabling iFolder User Accounts

**Time Required:** 10 minutes

**Objective:** Enable iFolder user accounts.

**Requirements:** Same as Activity 10-2

**Description:** Eric wants you to test the system by enabling iFolder user accounts for all users in the IT Department.

1. If necessary, start your computer, and log on with your local user name and password.
2. If necessary, start iFolder Management as described in Step 2 of Activity 10-2.
3. Click the **User Management** option and, if necessary, log in as your administrative user to open the window shown previously in Figure 10-14.
4. Click the **Advanced Search** link. In the In User LDAP: Context list box, click the **IT OU**.
5. Click the **Search** button to display the IT user accounts.
6. Click the **Enable all found users as iFolder users** button, and then click **OK** to enable all IT user accounts and return to the Advanced Search for Users window.
7. Exit iFolder Management, and close your Web browser.

## System Monitoring

Clicking the System Monitoring option provides a real-time view of the status of your iFolder environment (see Figure 10-17). You can see a list of all iFolder and LDAP servers in your network, including status, number of users, and available disk space.

Notice that this window contains a button for stopping the synchronization process, which might be necessary if the iFolder server needs to be shut down for repair or upgrades. After stopping synchronization, you must restart the iFolder server to resume automatic synchronization with the iFolder clients.
