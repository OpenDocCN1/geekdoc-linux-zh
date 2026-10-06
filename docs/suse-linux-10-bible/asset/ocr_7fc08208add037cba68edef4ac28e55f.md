either a success or failure back to the process (in this case imap) that tried to authenticate the user. It is this failure that will stop you from logging in for one reason or another, if there is a problem with your account (expiry, for example) or your authentication credentials (incorrect username or password).

The second field can be one of the following:

+   - required—If a failure is encountered by the module, it results in an overall failure of the PAM system for the service (imap). Even if the authentication fails, execution of the remaining definitions in the service configuration continues.
- requisite—If a failure occurs, PAM returns a failure immediately and stops executing the rest of the module in the configuration file.
- sufficient—If this PAM module returns a success from the system, it returns an overall success even if a previous PAM module returned a failure (useful to use with the required action).
- optional—If authentication succeeds or fails, it is enforced only if this is the only entry for this type of service (account, password, auth, or session).

The third and fourth fields are the location of the PAM module on the filesystem and any parameters you need to pass to the module. For example, if you want to authenticate users against a MySQL database (using pam_mysql), you need to pass the database name, table name and the user column, and also the username and password of the MySQL user that can connect to the database.

In the example we have for the imap service, we have said that for the auth and account methods, the authentication must succeed in both entries (which makes sense if the user and password are incorrect or the account has been disabled, we do not want the user to log in). Both of these entries use the pam-unix.so module, which queries the Standard Unix database (/etc/passwd and /etc/shadow). And finally for the auth entry, we told the pam-unix module that it is ok if the user enters with an empty password (if the user has a blank password— bad idea).

# Integrating LDAP into Linux

When you have user accounts stored in LDAP, you can authenticate your users against them. Three things need to take place to make this happen:

+   1. When the system needs to find information about a user (UID, home directory, or so on), it queries the name switch. The NSS is a core component