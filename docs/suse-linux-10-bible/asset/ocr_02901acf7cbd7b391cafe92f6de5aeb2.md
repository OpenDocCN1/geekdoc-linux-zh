If you ever need to find out what Cyrus commands can you use, type help in the Cyrus command shell.

| Table 17-1
yrus ACL Settings |
| ACL Code | Description |
|---|---|
| L | List the folder—that is, be able to view the folder in a folder list. |
| r | Read the contents of the folder. |
| s | Set the seen flag on a message in the folder. |
| w | Write to the folder—that is, store a message in the folder. |
| i | Insert or append a message to the folder. |
| p | Send a mail to the folder. |
| c | Create (subfolder) or delete the folder. |
| d | Delete a message in the folder. |
| a | Administrative rights on the folder, set ACLs. |

To set an ACL on the folder, you need three pieces of information: the user you want to set the ACL for, the mailbox, and the ACL settings themselves. Consider the example in Listing 17-5.

+   Listing 17-5: Setting ACLs on a Shared mailbox
- localhost> sam share aimee lrwip
- localhost> sam share roger lrwip
- localhost> sam share justin lrip
- localhost> lam share
- roger lrwip
- justin lrwip
- anyone lrs
- aimee lrwip

We, have allowed the users justin, roger, and aimee to list the folder, read the contents of the folder, the seen flag on a message, store a message in the folder, and also send a message directly to the folder. We have not allowed them to delete any messages in the folder, so all is as we orinally wanted.