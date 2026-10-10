# Activity 10-2: Viewing and Modifying iFolder Global Settings

**Time Required:** 10 minutes

**Objective:** Use the iFolder Management utility to access configuration information.

**Requirements:** Completion of Activity 10-1 or iFolder installed on the classroom server and Internet Explorer on a Windows XP computer or Java-enabled Firefox on a SUSE Linux 10 computer.

> If you're using iFolder from the classroom server, you need access to an iFolder administrative user account and password. If you don't have access to an administrative user account, your instructor might perform this activity as a class demonstration.

**Description:** In this activity, you use the iFolder Management console to document your iFolder configuration settings and add the IT OU to the iFolder search contexts.

+   1. If necessary, start your computer, and log on to your local computer.

+   2. Start your Web browser, and then start iFolder Management by entering the URL `https://IPaddress/iFolderServer/Admin` (replacing *IPaddress* with the IP address of your NetWare 6.5 OES server) to display the Novell iFolder menu options.

+   3. Click the **Global Settings** icon, and then enter your assigned iFolder user name and password to display the General Information window. (If you're using a dedicated server, enter your administrative user name and password.)

+   4. Record your default port and context:
+   _______________________________

+   5. Click the **Global Policies** link, and then click the **Client Policies Display** button. Record the default setting for Sync To Server Delay (sec):
+   _______________________________

+   6. Click your browser's **Back** button, click the **Server Policies Display** button, and enter **30** in the Session Timeout text box.

+   7. Click the **Update** button to apply your changes.

+   8. Click the **Admin Names** link, and record the iFolder administrators:
+   _______________________________

+   9. Click the **User LDAPs** link, and follow these steps to add the IT OU to the Contexts To Search list:
+       a. Click the *iFolder_ldap01* link to display the contexts to search (shown previously in Figure 10-12).
+       b. Click the **Add** button in the Contexts To Search row to display the Search for context to add window.
+       c. Enter **IT\*** in the Context Name text box, and then click the **Search** button to display a search results window showing your IT context.
+       d. Click the *IT.UAS* container, and then click the **Add** button to add the IT OU to the Contexts To Search list. (If you're using a classroom server, click *IT.#\#UAS* in the search results window, replacing *#\#* with your assigned student number.)
+       e. Click to select the check box next to the ITUAS context, and then click the **Update** button to apply your changes.
+       f. Click the **Home** button to return to the Novell iFolder main window.

+   10. You can leave the iFolder Management window open for the next activity. If you have finished your session, click the **Exit** button and then close your Web browser.