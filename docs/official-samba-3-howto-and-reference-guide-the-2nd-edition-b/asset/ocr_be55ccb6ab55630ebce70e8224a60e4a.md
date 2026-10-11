trusted machine account. Suppose, your domain is called SAMBA, and the remote domain is called RUMBA. The first step will be to issue this command from your favorite shell:

```
```
root# smbpasswd -a -i rumba
New SMB password: XXXXXXX
Retype SMB password: XXXXXXX
Added user rumba$
```
```

where -a means to add a new account into the passdb database and -i means to “create this account with the Interdomain trust flag”.

The account name will be “rumba$” (the name of the remote domain). If this fails, you should check that the trust account has been added to the system password database (`/etc/passwd`). If it has not been added, you can add it manually and then repeat the previous step.

After issuing this command, you will be asked to enter the password for the account. You can use any password you want, but be aware that Windows NT will not change this password until 7 days following account creation. After the command returns successfully, you can look at the entry for the new account (in the standard way as appropriate for your configuration) and see that the account’s name is really RUMBA$ and it has the “I” flag set in the flags field. Now you are ready to confirm the trust by establishing it from Windows NT Server.

Open User Manager for Domains and from the **Policies** menu, select **Trust Relationships...**. Beside the **Trusted domains** list box, click the **Add...** button. You will be prompted for the trusted domain name and the relationship password. Type in SAMBA, as this is the name of the remote domain and the password used at the time of account creation. Click on **OK** and, if everything went without incident, you will see the **Trusted domain relationship successfully established** message.

# ## 18.4.2 Samba as the Trusting Domain

This time activities are somewhat reversed. Again, we’ll assume that your domain controlled by the Samba PDC is called SAMBA and the NT-controlled domain is called RUMBA.

The very first step is to add an account for the SAMBA domain on RUMBA’s PDC.

Launch the Domain User Manager, then from the menu select **Policies. Trust Relationships**. Now, next to the **Trusted Domains** box, press the **Add** button and type in the name of the trusted domain (SAMBA) and the password to use in securing the relationship.

The password can be arbitrarily chosen. It is easy to change the password from the Samba server whenever you want. After you confirm the password, your account is ready for use. Now its Samba’s turn.

Using your favorite shell while logged in as root, issue this command:

```
`root#net rpc trustdom establish rumba`
```