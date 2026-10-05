# 10.3.4.5 Map Management

There is good news and bad news when it comes to map management. The good news is that you can edit the **passwd**, **group**, and **hosts** maps using Active Directory Users and Computers. (You can also use the *nisadmin* command.) The bad news is that for all other maps, you have to use the ADSI Edit utility in the Support Tools folder of the Windows 2000 media.

To edit **passwd**, **group**, and **host** maps using Active Directory, just start Active Directory Users and Computers and select the domain you want to edit. Then, for **passwd** and **group** maps, click **Users**. For the *hosts* map, click **Computers**. Right-click on the user or computer you want to edit, choose **Properties**, and select the **UNIX Attributes** tab to make your changes. See Figure 10–11 for a picture of the UNIX Make sure the NIS Domain box contains the name of the correct NIS domain. When creating a new user account or computer entry, this box will specify <none> by default. Just click on the arrow to the right of that box to select the NIS domain.

I would suggest not using the other maps. For my foray to ADSI Edit were fraught with frustration. Therefore, keep references to other information local until Microsoft comes up with an easier way to edit all other maps on Server for NIS.

# 10.4 Conclusion

If you are beginning to see potential for some real complexity developing here, you are right. In this and previous chapters we've seen a number of authentication schemes: local UNIX authentication, NIS, NTLM, Kerberos. In the next chapter, we turn to file sharing. File sharing involves authorization in addition to authentication. We can share files from UNIX systems to Windows systems using NFS or CIFS. We can do the same in the other direction. We have share permissions, NFS permissions, UNIX permissions, NTFS permissions. Whew!

Did I say this was going to be easy?

# References

+   1. Hal Stern and Mike Loukides, *Managing NFS and NIS*. (O'Reilly, 1997)
2. The Services for UNIX Help File