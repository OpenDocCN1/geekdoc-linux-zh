# # Accessing an LDAP Address Book from Thunderbird

With your LDAP address book configured and running, you should be able to use it to get e-mail addresses from any e-mail client that supports LDAP directories. Assuming that your LDAP directory is up and running, the following example shows how to use Thunderbird (which is available with CentOS distributions) to search your LDAP directory for e-mail addresses.

+   1. From Thunderbird, click on the “Address Book” button.

+   2. From the Address Book window, select **File** ➤ **New** ➤ **LDAP Directory**. From the Thunderbird Directory Server Properties window that appears, enter at least the following information on the General tab:

+   * **Name** — The name that identifies the server on your LDAP Servers List

+   * **Hostname** — The name or IP address of the computer hosting the LDAP content

+   * **Base DN** — Indicates the point in the LDAP directory to begin searching. You can select **Find** to have Thunderbird check your LDAP server for the Search Base. In the example, dc=example|le, dc=com is the search base.

+   * **Port** — Enter an IP address for the LDAP server. The port number is 389 by default.

Figure 21-1 shows the Directory Server Properties window that was just filled out.

# ## FIGURE 21-1

Enter information about your LDAP directory server to search for addresses from Thunderbird.

![](bbox=[0.14, 0.62, 0.96, 0.91])