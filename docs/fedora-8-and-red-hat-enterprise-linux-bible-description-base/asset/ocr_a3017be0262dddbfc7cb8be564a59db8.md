|   | Print out packets sent and received |
|---|--------------------------------------|
| 16|                                      |
| 32| Search filter processing |
| 64| Configuration file processing |
| 128| Access control list processing |
| 256| Stats log connections/operations/results |
| 512| Stats log entries sent |
| 1024| Print communication with shell backends |
| 2048| Entry parsing |

By default, the loglevel is 256. To log everything, set the loglevel to 4095. To get combinations of loglevel features, simply add the numbers you want together. For example, for trace function calls, heavy trace debugging and connection management, use the number 13 (as in 1 + 4 + 8).

+   • **Limit searches** — You can limit the number of entries that can be returned by a search (`sizelimit 500`, by default) and the amount of time `slapd` will take to answer a search request in seconds (`timelimit 3600`). Add new values that you want for your LDAP directory to your `slapd.conf` file.
+   
+   • **Add access control policy** — In the `slapd.conf` file, the default database access is set to allow read access by anyone who can access the database. If you want to change that behavior, you can add access lines to selectively decide who can read and write to your database. For this example, I want to allow everyone to be able to read from the database, but only allow people to change their own information. Refer to the `slapd.conf` man page for further information.

# ## Accessing an LDAP Address Book
## from Thunderbird

With your LDAP address book configured and running, you should be able to use it to get e-mail addresses from any e-mail client that supports LDAP directories. Assuming your LDAP directory is up and running, the following example shows how to use Thunderbird (which is available with Fedora and RHEL distributions) to search your LDAP directory for e-mail addresses.

+   1. From Thunderbird, click the Address Book button.
+   2. From the Address Book window, select `File → New → LDAP Directory`. From the Thunderbird Directory Server Properties window that appears, enter at least the following information on the General tab:

+   - **Name** — The name that identifies the server on your LDAP Servers list.
+   - **Hostname** — The name or IP address of computer hosting the LCAP content.
+   - **Port** — Enter an IP address for the LDAP server. The port number is 389 by default.