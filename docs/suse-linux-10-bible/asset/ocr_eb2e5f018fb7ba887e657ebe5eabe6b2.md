# 490 Part IV ♦ Implementing Network Services in SUSE Linux

New password:
Re-enter new password:
Password changed

When set, you need to start the cursus and laslauthd services. Cyrus is the Cyrus authentication daemon. SASL is a general-purpose authentication mechanism that can be used in client and server environments. Cyrus IMAP relies on the SASL library to provide authentication services.

# Adding Users to Cyrus

When those users are started, you need to add users to the Cyrus Database to provide mail services for them. We will take the user justin (who must exist in the system) as add a user to the Cyrus system, become the Cyrus user and connect to the Cyrus IMAP server with the cyradm command (Cyrus administration):

```
bible: # su - cyrus
cyrusservice-> cyradm localhost
IMAP Password:
localhost>
```

When connected, you can use the cm (create mailbox) command to create the user justin's inbox:

```
localhost> cm user.justin
localhost> lm
user.justin (HasNoChildren)
localhost>
```

Here have told Cyrus to create the mailbox user.justin. This may seem odd, but it is a standard way to configure Cyrus for mailboxes. Cyrus works on a hierarchical mailbox structure, not only for the users, but also for system mailboxes. These system mailboxes could be mailboxes that are shared between many users for bulletins, for example.

# Creating a Shared Mailbox

If you want to create a mailbox that is shared between certain users, use the cm command to create the mailbox and also set the access control list (ACL) for users on the mailbox.

For example, if you have three users, justin, roger, and aimee, on the system, and you want them to be able to store and view messages in this folder, but not to be able to delete any, you can look up the access control codes in Table 17-1 and set the ACL on that folder using the sam command (set ACL on folder).