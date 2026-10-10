Now you're set up to use ssh login to the server. If everything was done correctly, you'll be prompted for your pass phrase when you log in, instead of your password. **Connecting to the same server from several client hosts**: To do this, you'll need to repeat the foregoing steps for each client. When you do, make these changes:

+   ▼ In step 3, use another filename rather than Local.pub.
+   ▲ In step 4, the authorization file should be appended to rather than re-created for each new client host. You can append to the file by opening it with your favorite editor and adding the new lines to the bottom of the file.

# APPLICATIONS RELATED TO SSH

The SSH2 package actually comes with two additional programs that use the same en-cryption technology.

+   ■ **Secure Copy (scp)**: Secure Copy is meant as a replacement for the rcp command, which allows you to do remote copies from one host to another. The most significant problem with the rcp command is that users tend to arrange their remote-access settings to allow far too much access into your system. To help mitigate this, instruct users to use the scp command instead. The format of scp is identical to rcp, so users shouldn't have problems with this transition.

> NOTE: The scp program comes with SSH1 as well as SSH2.

+   ■ **Secure FTP Transfers (sftp)** Another useful application that comes with SSH2 is the sftp client, which allows you to perform secure FTP transfers. It works very much like the normal FTP client, so users will be able to make this transition easily. The most signifi-cant drawback to sftp is that there is no standard for performing secure FTP transfers; thus sftp works only with sites that are running the corresponding SSH2 daemon.
+   ■ Migrate your users to scp and sftp, and you'll have made a significant step toward making your system more secure.

# SUMMARY

The Secure Shell tool is a superior replacement to Telnet for remote logins. Adopting the SSH package will put you in the company of many other sites that are disabling Telnet ac-cess altogether and allowing only SSH access through their firewall. Given the wide-open nature of the Internet, this change isn't an unreasonable thing to ask of your users. Here are the key issues to keep in mind when you consider Secure Shell.

+   ▼ SSH is very easy to compile and install.
+   ■ Replacing Telnet with SSH requires no significant retraining.