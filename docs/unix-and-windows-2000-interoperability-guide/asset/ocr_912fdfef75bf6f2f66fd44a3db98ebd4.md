# CIFS/9000 Server in a Windows 2000 Domain

There are other steps you might need to take, such as registering your server with Windows Internet Naming Service (WINS). Windows 2000 still supports WINS. Using WINS can make your life a lot easier. in smb.conf, you can specify your WINS server with the wins parameter, which to supply either the DNS name or IP address of your WINS server.

# 12.4.1.2 How It Works

We have our CIFS/9000 member of a Windows 2000 domain. By configuring smb.conf the way we have, we specify that client requests to the CIFS/9000 server will first be authenticated by the Windows 2000 domain controller. On top of all that, we we have our Windows 2000 domain controller running for NIS.

In my environment, this setup works well. If I log into a Windows 2000 client as an everyday user, say dylan, the domain controller authenticates me, as you would expect. Then, when I browse the network, I click on the book.local domain icon. One of the servers I see is hpux. My CIFS/9000 server. Double-clicking on that icon shows me a list of shares available. In my initial configuration, the only share I see is one called dylan. Where did it come from?

By default, CIFS provides a shared definition called home in smb.conf. If a user's home directory exists on the server it will create a temporary share configured with the parameters from the home definitions so that the user can access that home directory. How does it determine the home directory? Either by scanning /etc/passwd or consulting an NIS map. In my case, the user dylan is defined in an NIS map maintained by Server for NIS. I created this user using Active Directory for Users and Computers, being the UNIX Attributes so that dylan was defined in NIS as well. See Figure 12-2.

Therefore, upon logging in as dylan, CIFS/9000 sees that dylan's home directory actually exists on the CIFS/9000 server, a share with the name dylan is created. Here is an important point. All Windows 2000 users whose home-directories are to be served by CIFS/9000 must actually have those directories created for them by the root user. For example, when creating a new user account lucky, I used Active Directory Users and Computers to do so. However, I also had to issue the following commands as root on hpux, my CIFS/9000 server:

```
# cd home
# mkdir lucy
# chown lucy:tech lucy
# ls -l
total 6
drwxrxr-x 3 dylan tech 1024 Dec 22 05:30 dylan
drwxrxr-x 4 hilary tech 1024 Dec 21 22:19 hilary
drwxrxr-x 2 lucky tech 1024 Dec 22 05:54 lucky
```