3. The kinit program then prompts you to enter your Kerberos password, which it then uses to decrypt the TGT. You can manage your Kerberos password with the kpasswd command.

4. Now you can use a client program such as a mail client program to access the mail server, for instance. When you do so, the TGT is used to access the TGS, which then will generate a ticket for accessing the mail server. The TGS will generate a new session key for use with just the mail server. This will be provided in the ticket sent to you for accessing the mail server. In effect, there is a TGT session key used for accessing the TGS, and a mail session key used for accessing the mail server. The ticket for the mail server is sent to you encrypted with the TGS session key.

5. The client then uses the mail ticket received from the TGS to access the mail server.

6. If you want to use another service such as FTP, when your FTP client sends a request to the TGS for a ticket, the TGS will automatically obtain authorization from the authentication server and issue an FTP ticket with an FTP session key. This kind of support remains in effect for a limited period of time, usually several hours, after which you again have to use kinit to undergo the authentication process and access the TGS. You can manually destroy any tickets you have with the kdestroy command.

> NOTE With Kerberos V5 (version 5), a Kerberos login utility is provided whereby users are automatically granted ticket-granting tickets when they log in normally. This avoids the need to use kinit to manually obtain a TGT.

# Kerberized Services

Setting up a particular service to use Kerberos (known as Kerberizing) can be a complicated process. A Kerberized service needs to check the user’s identity and credentials, check for a ticket for the service, and if one is not present, obtain one. Once they are set up, use of Kerberized services is nearly transparent to the user. Tickets are automatically issued and authentication carried out without any extra effort by the user.

# Configuring Kerberos Servers

Installing and configuring a Kerberos server is also a complex process. Carefully check the documentation for installing the current versions. Some of the key areas are listed here. In the Kerberos configuration file, krb5.conf, you can set such features as the encryption method used and the database name. When installing Kerberos, be sure to carefully follow the instructions for providing administrative access. The /etc/services file should contain a listing of all Kerberized services. These are services such as kftp or klogin that provide Kerberos FTP and login services. To run Kerberos, you start the Kerberos server with service command and the krb5kdc, kadmind, and krb524 scripts.

> TIP Check the Red Hat Linux Reference Manual for more detailed instructions on setting up Kerberos servers and clients on your system.

Consult the Red Hat Linux Reference Guide for detailed instructions on how to install and configure Kerberos on Red Hat. You will need to configure the server for your network, along with clients for each host. To configure your server, you first specify your Kerberos