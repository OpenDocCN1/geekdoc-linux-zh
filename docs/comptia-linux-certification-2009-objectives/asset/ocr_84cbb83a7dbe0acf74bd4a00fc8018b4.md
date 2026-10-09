2. Enable the Telnet server.

+   a. Enter **vi /etc/xinetd.d/telnet** to open the telnet configuration file.

+   b. Observe that the default configuration entries are displayed. Also, observe that the service is disabled as indicated by **disable=yes**.

+   c. Enter **/dis** to navigate to the "disable = yes" line.

+   d. Switch to the insert mode.

+   e. Change **disable = yes** to **disable = no**

3. Enable access control for the Telnet service.

+   a. On a new line, press the **Tab** key.

+   b. Enter **only_from** and press the **Tab** key. Enter **= 192.168.0.0/24** to allow the service to be accessed only from 192.168.0.0.

+   c. Press the **Tab** key and enter **no_access**. Press the **Tab** key and enter **= 192.168.0.205** to deny access to the service for all users from 192.168.0.205.

+   d. Switch to the command mode.

+   e. Save and close the file.

4. Configure xinetd to start at system boot.

+   a. Enter **service xinetd start** to start the xinetd service.

+   b. Enter **chkconfig xinetd on** to enable the xinetd service to start at system startup.

+   c. Clear the terminal screen.