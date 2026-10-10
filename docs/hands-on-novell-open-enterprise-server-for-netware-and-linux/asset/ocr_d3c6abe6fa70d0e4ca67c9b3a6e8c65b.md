7. If necessary, click the **Client** tab to select it, as shown in Figure 4-28. Notice the text boxes for First network drive, Preferred server, and Preferred tree. These text boxes can be used to change the default settings when a user first logs in. In addition, the Client tab contains the version number of the client and the latest service pack. This information is important to ensure that the client is current. The bottom section of the Client tab contains the default context where eDirectory looks to find the user name.

+   4

![](bbox=[0.09, 0.18, 0.51, 0.45])

Figure 4-28 Options in the Client tab

8. Verify that the First network drive is set to F and that the Preferred tree text box contains UAS_TREE. (Your tree name might vary if you're using your own server.)

9. Follow these steps to change the default context so that it points to the Engineering container in the UAS Organization:

+   a. In the Tree text box, enter your eDirectory tree name (*UAS_TREE* if you're using a shared classroom server or your eDirectory tree name if you're using a dedicated server).

+   b. In the Name context text box, enter **UAS**. (If you're using a shared classroom server, enter the context of your UAS container, such as .##UAS.CLASS.)

+   c. Click the **Add** button to insert the context.

10. Click the **Advanced Login** tab, where you set which options are displayed when you click the Advanced button during login. Record the current settings here:

11. Click the **Advanced Menu Settings** tab, where you can set the options available on various menus. If necessary, click the **Change Password** option, and then record the description here:

12. Click the **Advanced Settings** tab, where you control parameters used to communicate on the network. Click the **File Caching** option, and then record the description here:

13. Click the **LDAP Contextless Login** tab, which is used to specify a global catalog of objects. The global catalog makes it possible to log in or access a resource without specifying which container the user account or resource is located in. Record whether contextless login is enabled on your computer: