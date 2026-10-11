
-   • GroupWise® Configuration
-   • Lotus® Notes® Configuration
-   • Microsoft® Exchange Configuration
-   • NetMail Configuration
-   • IMAP/POP3 Server Configuration
-   • Public Web Page
-   • Change Password

## Company Info Service

The News feature lets you post information in the Virtual Office News field on the home page.

Do the following:

1.  Open iManager.
2.  Select **Virtual Office Management > Services Administration > Company Info**.

The following appears:

![](img/d63035f3fce0eaaf97203dde900affb7_236_0.png)

![](img/d63035f3fce0eaaf97203dde900affb7_236_1.png)

3.  **Mark Enable.** If unchecked, the Virtual Office News field does not appear on the home page.
4.  **Type the *message* you want in the News field.** You can use either plain text or HTML.
5.  **Select OK.**

## NetStorage

The NetStorage tab lets you access Novell NetStorage, which provides simple Internet-based access to files on your server. To configure this, complete the following:

1.  **Open iManager.**
2.  **Select *Virtual Office Management* > *Services Administration* > *NetStorage*.**

The following appears:

![](img/d63035f3fce0eaaf97203dde900affb7_237_0.png)

3.  **Mark Enable**.

    If unchecked, the *Files* icon does not appear in Virtual Office.

4.  Do one of the following to specify the *URL* to the NetStorage main page:
    -   If NetStorage is on the same server, select **Launch to this server’s NetStorage Home Page**.
    -   If NetStorage is on a remote server, specify the *DNS* or *IP address* of the remote server.
        -   For example, `https://DNS_ or _IP_Address:443/NetStorage/servlet/NetStorage`
    -   Enter a custom *URL* to launch NetStorage.

With some browsers (including Mozilla 1.5, Internet Explorer 6.1 SP1, and Netscape 7.01 and 7.02), the URL you enter for your NetStorage Web page in the Virtual Office Services Administration plug-in is not saved.

If the URL you enter is not saved, try a different browser. Internet Explorer 6 and Netscape 7.1 are known to work.

## iPrint

iPrint is a software solution that lets users print from anywhere to anywhere.

To configure this, do the following:

1.  Open iManager.
2.  Select **Virtual Office Management > Services Administration > iPrint**.

The following appears:

![](img/d63035f3fce0eaaf97203dde900affb7_238_0.png)

# Figure 9-6

3.  Mark **Enable**.
    If unchecked, the iPrint icon does not appear in Virtual Office.

4.  Do one of the following to specify the *URL* to the iPrint Web site:
    -   If iPrint is on the same server, click **Launch to this server’s iPrint Home Page**.
    -   If iPrint is on a remote server, specify the *DNS* or *IP address* of the remote server.
        -   For example, `https://DNS_ or _IP_Address/iPrint/servlet/iPrint`
    -   Specify a custom *URL* to launch iPrint.

5.  Select **OK**.

## eGuide

Novell eGuide is a Web application that provides a browser-based search capability for users regardless of the location of your LDAP data source.

To configure eGuide, do the following:

1.  Open iManager.
2.  Select **Virtual Office Management > Services Administration > eGuide**.

The following appears:

# Figure 9-7

![](img/d63035f3fce0eaaf97203dde900affb7_240_0.png)

3.  Mark **Enable**.

    If this box is unchecked, the eGuide icon does not appear in Virtual Office.

4.  Do one of the following to specify the *URL* to the eGuide Web:
    -   If eGuide is on the same server, click **Launch to this server's eGuide Home Page**.
    -   If eGuide is on a remote server, specify the *DNS* or *IP address* of the remote server.
        -   For example, `https://DNS_or_IP_Address/eGuide/servlet/eGuide`
    -   Specify a custom *URL* to launch eGuide.

5.  Select **OK**.

You can also set an optional proxy URL. This allows an Internet proxy/accelerator, like Novell iChain, to correctly rewrite the specified proxy URL to the correct DNS name that will allow a user's browser to work properly through the proxy server.

## ZENworks

ZENworks provides directory-based management of desktops, handheld devices, and servers.

To use ZENworks with **Virtual Office**, you must install and configure Novell ZENworks 6 Desktop Management and Web Self-Service components.

![](img/d63035f3fce0eaaf97203dde900affb7_241_0.png)

See http://www.novell.com/documentation/ig/zenworks6/index.html for more information.

To configure ZENworks access through **Virtual Office**, do the following:

1.  Open **iManager**.
2.  Select **Virtual Office Management** > **Services Administration** > **ZENworks**.

    The following appears:

    **Figure 9-8**

    ![](img/d63035f3fce0eaaf97203dde900affb7_241_1.png)

3.  Mark **Enable**.

4.  Specify the *URL* for the ZENworks Web page.
5.  Select **OK**.

## Bookmarks

The Bookmarks tab page provides configuration options for the Virtual Office Bookmarks service.

To configure this, do the following:

1.  Open iManager.
2.  Select **Virtual Office Management > Services Administration > Bookmarks**.

    The following appears:

    ![](img/d63035f3fce0eaaf97203dde900affb7_242_0.png)

3.  If you want the **Bookmarks** button to appear in the Virtual Office button bar, to the right of the **Bookmarks Link** title select **Enable**.

4.  If you want bookmarks to appear on user home pages, to the right of the Home Page Bookmarks title select **Enable** and do 1 or more of the following:
    -   Add a bookmark by selecting **Add**; then enter a bookmark *name* and *URL* and select **OK**.
    -   Edit an existing bookmark by selecting the *bookmark* and selecting **Edit**; then change the *name* or *URL* of that bookmark and select **OK**.
    -   Delete an existing bookmark by selecting the *bookmark*; then select **Delete**.

5.  Select **OK**.

## GroupWise® Configuration

This parameter provides configuration settings for the Virtual Office GroupWise option.

To configure this, do the following:

1.  Open iManager.
2.  Select **Virtual Office Management > Services Administration** > eMail.
3.  If you want the e-Mail button to appear in the Virtual Office button bar, to the right of the eMail Link title select **Enable**.
4.  From the Email Server menu, select **Novell GroupWise**.
5.  Select **Edit**.
6.  Enter the GroupWise WebAccess *URL*.
7.  If the user's credentials are the same as those used by the Virtual Office eDirectory tree, select **Synchronized with Virtual Office Tree**.
8.  Select **OK**.

9.  You can also configure the Home Page Reduced eMail View. When the reduced email view is enabled, the user's most recent email will be listed on the user's Virtual Office Home Page.
    Do the following:
    -   a. Configure your GroupWise server to support POP3 or IMAP.
    -   b. To the right of the Home Page Reduced eMail View title select **Enable**.
    -   c. Select *Edit*.
    -   d. Select **POP3** or **IMAP**.
    -   e. Enter your Incoming Mail Server *DNS name* or *IP address*.
    -   f. Enter your SMTP Server *DNS name* or *IP address*.
    -   g. If the user's credentials are the same as those used by the Virtual Office eDirectory tree, select **Synchronized with Virtual Office Tree**.
    -   h. Select **OK**; then select **OK**.

## Lotus® Notes® Configuration

This parameter provides configuration settings for the Virtual Office Lotus Notes option.

To configure this, do the following:

1.  Open iManager.
2.  Select **Virtual Office Management > Services Administration > eMail**.
3.  If you want the e-Mail button to appear in the Virtual Office button bar, to the right of the eMail Link title select **Enable**.
4.  From the E-mail Server menu, select **Lotus Notes**.
5.  Select *Edit*.
6.  Specify the Lotus Notes *URL*.
7.  Specify the Lotus Notes *proxy address*.

8.  Select **OK**.

9.  You can also configure the Home Page Reduced eMail View. When the reduced email view is enabled, the user's most recent email will be listed on the user's Virtual Office Home Page. Do the following:
    -   a. Configure your Notes server to support POP3 or IMAP.
    -   b. To the right of the Home Page Reduced eMail View title select **Enable**.
    -   c. Select *Edit*.
    -   d. Select **POP3** or **IMAP**.
    -   e. Enter your Incoming Mail Server *DNS name* or *IP address*.
    -   f. Enter your SMTP Server *DNS name* or *IP address*.
    -   g. If the user's credentials are the same as those used by the Virtual Office eDirectory tree, select **Synchronized with Virtual Office Tree**.
    -   h. Select **OK**.

10. Select **OK**.

## Microsoft® Exchange Configuration

This parameter provides configuration settings for the Virtual Office Exchange option. To configure this, complete the following:

1.  Open iManager.
2.  Select **Virtual Office Management > Services Administration > eMail**.
3.  If you want the e-Mail button to appear in the Virtual Office button bar, to the right of the eMail Link title select **Enable**.
4.  From the E-mail Server menu, select **Microsoft Exchange**.
5.  Select *Edit*.
6.  Specify the Microsoft Exchange *URL*.
