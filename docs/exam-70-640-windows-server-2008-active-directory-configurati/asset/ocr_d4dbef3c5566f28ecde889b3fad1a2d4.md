# Table 5-2
Special Identity Groups

| GROUP NAME | MEMBERS | PURPOSE |
| :--- | :--- | :--- |
| Anonymous Logon | All users who log on without a username and password | Used to allow anonymous users access to resources. Windows Server 2008 no longer includes the Anonymous Logon group as a member of the Everyone group. This security enhancement prevents the potential for unauthorized access to resources that can occur if a Windows 2000 or earlier administrator forgets to remove the Everyone group from a resource. |
| Authenticated Users | All users who log on with a valid username and password combination that is stored in the Active Directory database | Used to allow controlled access to resources throughout the forest or domain. |
| Batch | Users who are logging on to a server as a batch job. | Used to facilitate users who need to log on as a batch job (i.e., to run a scheduled task on a Windows Server 2008 computer). |
| Creator Group | The primary group that is configured for the creator of an object. | Used as a placeholder for the primary group of an object's creator. |
| Creator Owner | The user that created a particular object. | Used to grant permissions to the creator of an object. |
| Dial-Up | Includes users currently logged on using a dial-up connection | Used to allow access to resources from a remote location. |
| Digest Authentication | Users who are authenticating using Digest authentication | Used to control access to a resource based on the type of authentication being used. |
| Enterprise Domain Controllers | All domain controllers in the forest | Used to facilitate access to forest-wide Active Directory services. |
| Everyone | On Windows Server 2003 and later computers: Authenticated Users Domain Guests On Windows NT Server 4.0 and Windows 2000 computers: Authenticated Users Domain Guests Anonymous Logon | Used to provide access to resources for all users and guests. Do not assign this group to resources. Instead, use groups that require authentication and have membership lists that can be administratively modified. |
| Interactive | Includes the user account that is currently logged on to the local computer either directly or through a Remote Desktop connection | Provides access to physically local resources. Users logged on from across the network are not included in this group membership. |
| IUSR | N/A | Used as the built-in account for Internet Information Services (IIS). |
| Local Service | N/A | Used as a reduced-privilege account to allow applications to run on a server without requiring administrative access. The Local Service does not have any permissions to network resources, only the local server. |
| Network | Includes any user that currently has a connection from another computer to a network resource, such as a shared folder, on this computer. | Used to allow access to shared resources or services from across the network. Users logged on interactively are not included in this group membership. |

(continued)