# **Hands-On Projects**

# ## Hands-on Project 11-1: Creating a Web Site

Eric wants you to create a demonstration Web site for the Engineering Department. He plans to use it at the next management meeting to show managers how to use the Web server to access other Web pages by supplying the Web site name after the Universal AeroSpace URL. The Web site should simply consist of a heading and a simple graphic in the IT\Web\Engineer directory. Follow these steps:

+   1. If you’re using a shared classroom server, ask your instructor for the path to your virtual document directory. If you’re using a dedicated server, create a virtual document directory by following these steps:
+   
+      a. Start your Web browser, and enter the URL `https://IPaddress:2200` (replacing `IPaddress` with the IP address of your server). If necessary, click **Yes** to close the security alert message box and open the Login window. Enter your administrative user name and password and then click **Login**.
+   
+      b. Click to expand the **Open Source** heading on the left, and then click the **Apache 2.0** link. Click **Administer Single Apache Server** under the Apache 2.0 Links heading on the right to display the Server Status window.
+   
+      c. Click the **Content Management** button, and then click **Additional Document Directories**.
+   
+      d. Enter **Engineering** in the URL prefix text box. (If you’re using a shared classroom server, precede “Engineering” with your assigned student number.)
+   
+      e. Enter the path to your CORP:\IT\Web\Engineer directory in the Map To Directory text box.
+   
+      f. Click **Save** to open the Save and Apply Changes dialog box. Click **Save and Apply** to apply your changes to the Httpd.conf file and display the Success! message box. Click **OK** to return to Apache Manager.

+   2. Copy the **Radiance.jpg** file from the C:\WINNT\Web\Wallpaper directory to your CORP:\IT\Web\Engineer directory.

+   3. Create a simple HTML document that displays the Radiance.jpg file with the heading “Universal AeroSpace.”

+   4. Save the document as **Index.html** in your CORP:\IT\Web\Engineer directory.

+   5. Test the Web site by starting your Web browser and then entering the URL `https://IPaddress/Engineering` (replacing `IPaddress` with the IP address of your server and preceding “Engineering” with your assigned student number if you’re using a shared classroom server).

+   6. After your test document is displayed, have your instructor check your work.