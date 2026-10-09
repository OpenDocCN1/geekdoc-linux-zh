# ## ACTIVITY 13-1
### Configuring a Web Server

**Before You Begin:**

+   1. On srvA, you have logged in as root in the GUI.
2. The terminal window is displayed.
3. Enter `cd /root` to navigate to the root directory.
4. On the terminal window, copy the `english.html` file and the `Our Global Company_files` directory from the `/085039Data/Web_Services` directory to the `/var/www/html` directory.
5. Clear the terminal window.

**Scenario:**

Your company runs a chain of retail stores and wants to set up an online web store, which will provide information about the store and facilitate online shopping. Now, you want to configure the web server to facilitate web hosting. Also, you want to configure the web server in such a way that PHP pages are included in the website.

# What You Do

# How You Do It

| 1. Check whether httpd has been installed on the system. | a. Verify that the apr package has been installed on the system. |
| | b. Verify that the postgresql-libs package has been installed on the system. |
| | c. Verify that the apr-util package has been installed on the system. |
| | d. Verify that the httpd package has been installed on the system. |
| | e. Clear the terminal window. |
| 2. Enable PHP support on the system. | a. Enter `yum localinstall /rhelsource/Server/=> php-common-5.1.6-23.el5.i386.rpm` to install the php-common package. |
| | **Note:** The `=>` symbol is used in the step only to bring the step to the next line. It is not part of the code and therefore, students need not type the symbol. |