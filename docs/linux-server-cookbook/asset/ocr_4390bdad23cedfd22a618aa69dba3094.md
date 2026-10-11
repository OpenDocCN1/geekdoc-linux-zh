redirect the request to the command `mount.cifs`. The command `mount.cifs` is part of the package named **cifs-utils**. Some of the popular options available are the following:

+   * **username (or user)**: Specifies the username to connect to the server.
+   * **password (or pass)**: Specifies the password for the username.
+   * **domain (or dom or workgroup)**: Specifies the domain (workgroup) of the user
+   * **credentials (or cred)**: Specifies a file that contains the username and the password to authenticate to the server. It is also possible to specify the domain.
+   * **ro**: Mount as read-only.
+   * **rw**: Mount as read-write.
+   * **sec**: Security mode used; some options are *krb5*, *krb5i*, *ntlm*, and *ntlmv2*.
+   * **vers**: Specify the version of the protocol.

*Figure 10.13* shows an example of mounting the previously shared resource, specifying the username and the password as options. The output of the command **mount** is shown to list the default options:

```
```
[root@rhel ~]# mount -t cifs -o rw,username=agonzalez,password=Start123 \
> //192.168.122.43/storage/ /exported
[root@rhel ~]# mount |grep "/exported"
//192.168.122.43/storage/ on /exported type cifs (rw,relatime,vers=3.1.1,cache=str
ict,username=agonzalez,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.122.43,fil
e_mode=0755,dir_mode=0755,soft,nounix,serverino,mapposix,rsize=4194304,wsize=4194
304,bsize=1048576,echo_interval=60,actimeo=1)
```
*Figure 10.13: Example usage of the command mount*
```

It is recommended to use the option **credentials (or cred)** to specify a protected file containing the username and the password. An example of the file is as follows:

```
```
username=agonzalez
password=Start123
```
```

# ### FTP server and client

The **File Transfer Protocol (FTP)** is a historical protocol published for the first time in 1971. It is used to share files to end users mainly. Nowadays, the popularity of FTP is low, and it is mainly used to distribute software publicly. The