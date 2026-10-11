The following demonstrates the addition of an account to the server FR0DD:

```
```bash
root# net rpc user add jacko -S FR0DD -Uroot%not24get
Added user jacko
```
```

The account password can be set with the following methods (all show the same operation):

```
```bash
root# net rpc password jacko f4sth0rse -S FR0DD -Uroot%not24get
root# net rpc user password jacko f4sth0rse \
       -S FR0DD -Uroot%not24get
```
```

# ### 12.4.2 Deletion of User Accounts

Deletion of a user account can be done using the following syntax:

```
```bash
net [<method>] user DELETE <name> [misc. options] [targets]
```
```

The following command will delete the user account jacko:

```
```bash
root# net rpc user delete jacko -Uroot%not24get
Deleted user account
```
```

# ### 12.4.3 Managing User Accounts

Two basic user account operations are routinely used: change of password and querying which groups a user is a member of. The change of password operation is shown in Section 12.4.1.

The ability to query Windows group membership can be essential. Here is how a remote server may be interrogated to find which groups a user is a member of:

```
```bash
root# net rpc user info jacko -S SAURON -Uroot%not24get
net rpc user info jacko -S SAURON -Uroot%not24get
Domain Users
Domain Admins
Engineers
TorridGroup
BOP Shop
Emergency Services
```
```