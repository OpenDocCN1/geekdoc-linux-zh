# Running Red Hat Setup Agent

The first time you boot Red Hat Linux, after it is installed, the Red Hat Setup Agent runs to configure some initial settings for your computer.

> NOTE: The Red Hat Setup Agent only runs automatically if you have configured Red Hat Linux to boot to a graphical login prompt. To start it from a text login, log in as root and switch to init state 5 temporarily (type init 5). Log in to the graphical prompt. From a Terminal window as root user, type:
> ```
> # rm /etc/sysconfig/firstboot
> # /usr/sbin/firstboot
> ```

The first screen you see is the Welcome screen. From there, click the Next button to step through each procedure as follows:

+   **Date and Time Configuration** — You can manually enter the date (click on the calendar) and time (select hour, minutes, and seconds) or use the network time protocol to have your date and time set automatically from a known time server. Click on Enable Network Time Protocol (NTP), then select a time server by clicking on the down arrow and selecting a site. Network Time Protocol (NTP) is a service that allows computers to synchronize their date and time clocks with reliable time servers.

> TIP: Red Hat offers two time servers you can use (click the down arrow in the server box to see them). Or you can type in your own time server. It is better to type an IP address than a name for your time server.

Setting NTP in this way adds your chosen NTP server to the `/etc/ntp.conf` file (see the *server* option). To check that time has been synchronized, type the `ntptrace` command. You should not have to change your firewall for NTP to work, because NTP attempts to punch a hole through your firewall to synchronize your time.

+   **User Account** — For your daily use of Red Hat Linux, you should have your own user account. You should typically log in with this user name (of your choosing) and use only the root user to perform administrative tasks. In the first of the four text boxes on the screen, type a user name (something like j *parker* or *alanb*). Next, type your full name (like John W. Parker or Alan Bourne). Then type your password in the Password box and again in the Confirm Password box. Click Forward.

If some form of network authentication is used, such as LDAP, Kerberos, or SMB authentication, you can click the Use Network Login button. See the “Enabling Authentication” sidebar for information on choosing different authentication types.

# Enabling Authentication

In most situations, you will enable shadow passwords and MD5 passwords (as selected by default) to authenticate users who log in to your computer from local passwd and shadow password files. To change that behavior, you can select the Use