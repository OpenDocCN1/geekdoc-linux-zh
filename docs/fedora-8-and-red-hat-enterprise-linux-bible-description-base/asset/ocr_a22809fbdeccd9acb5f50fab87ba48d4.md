The rootdn line indicates that root access can be granted to change data in databases associated with the `linuxt0ys.net` distinguished name (provided the password is supplied with `rootpw`, as described in the next step). I added the last four options to improve performance of the bdb database (type `man slapd-bdb` for details).

+   **4. Add a password.** In the `slapd.conf` file, you need to enter the password that is required to modify your OpenLDAP backend database. By default, the `rootpw` line defines a clear-text string that is your password. The password will give you full control of the backend database. It will look something like the following:

```
rootpw    mysecret
```

> **NOTE:** If you are going to use a clear-text password, you should make sure that your `slapd.conf` file has read permissions closed to the world (`chmod 640 /etc/openldap/slapd.conf`). See the sidebar “Creating an Encrypted Password” for information on creating an encrypted password to access your OpenLDAP backend database.

# Creating an Encrypted Password

To create an encrypted password for the administrator of the OpenLDAP database you can use the `slappasswd` command. You can create the password using Crypt, SSHA, SMD5, MD5, or SSH encryption. Here’s an example of creating a password for OpenLDAP using MD5 encryption:

```
```bash
# slappasswd -h {md5} > /tmp/myslap
New password:  ******
Re-enter new password:  ******
# cat /tmp/myslap
{MD5}uBoM+LCQg5GHJ2Z4NLu9A==
```
```

Enter a password (twice) to create an encrypted MD5 password. This example directs the encrypted password into the `/tmp/myslap` file; you can read into the `slapd.conf` file later. In this example, I had you `cat` the file so you could see what the encrypted password looks like. Your password will be different. Here’s what the `rootpw` line will look like with an encrypted, rather than a clear-text password:

```
rootpw    {MD5}uBoM+LCQg5GHJ2Z4NLu9A==
```

+   **5. Save slapd.conf.** Save your changes to the `slapd.conf` file and close it.

+   **6. Check slapd.conf.** You can check for syntax errors in your `slapd.conf` file by running the `slaptest` command, as follows:

```
```bash
# slaptest -u
config file testing succeeded
```
```