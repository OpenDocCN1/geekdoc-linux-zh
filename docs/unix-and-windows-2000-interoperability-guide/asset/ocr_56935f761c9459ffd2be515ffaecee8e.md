# References

possibilities for handling the root user is to keep the su command configured for UNIX authentication or to use /etc/pam_user.conf for that account. See the pam.conf man page for more information.

As with the CIFS/9000 server, the client seems to work well with Server for NIS. Again, this effectively unifies the user databases of Windows 2000 and HP-UX. Otherwise, for PAM NTLM and PAM Kerberos, you need user accounts defined in both environments. While NIS running on HP-UX can consolidate your UNIX accounts. Server for NIS can consolidate those accounts with Active Directory.

# 12.6 Conclusion

We've looked at CIFS file sharing in this chapter by focusing on HP's CIFS/9000, the server portion which is based on Samba. We looked at both the server and found that a Windows 2000 domain controller can do all the authenticating. For the server, we can specify in /etc/opt/samba/smb.conf that the domain controller will do the authenticating. For the client, we can specify NTLM or Kerberos authentication. On top of all that, we see that Server for NIS can help us achieve a unified user database by combining NIS maps with Active Directory and can be used in conjunction with CIFS/9000. While there may be some details we haven't covered here, we have enough to provide a proof-of-concept on a couple of ways to use CIFS/9000.

# References

+   1. Marshall Kirk McKusick, Keith Bostic, Michael Karels, and John Quarterman, The Design and Implementation of the 4.4BSD Operating System. (Addison-Wesley, 1996).
2. Richard Sharpe, Tim Potter, and Jim Morris, Special Edition: Using Samba. (Que, 2000).
3. Hewlett-Packard, Installing and Administering the CIFS/9000 Client. (Hewlett-Packard, 2000).
4. Hewlett-Packard, Installing and Administering the CIFS/9000 Server. (Hewlett-Packard, 2000).