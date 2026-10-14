
## IMPORTANT:

As the System Administrator can create member-specific files in other directories, such files must be manually removed after the completion of clu_delete_member command.

- It removes the soon-to-be deleted member’s host name for its cluster interconnect interface from the /./rhosts and /etc/hosts.equiv files.
- It writes a log file, clu_delete_member.log, in the /cluster/admin directory.

The clu_delete_member command can be run either interactively or with a simple command line argument. For example, to delete member3 from a cluster, use the following command:

```
/usr/sbin/clu_delete_member -m 3
```

## 11.7.2 Steps to Deleting a Cluster Member

Now that we know what the clu_delete_member command actually does, let’s go over the actual steps needed to delete a cluster member.

- 1. First, we need to determine whether the member-to-be-deleted is a critical voting member of the cluster. This is an essential step since we do not want to impact the cluster’s operation by losing quorum.
  
  Before halting the member-to-be-deleted, we use the clu_quorum(8) command to determine whether it is safe to do so.
  
- 2. Shut down the cluster member-to-be-deleted.
  
- 3. Make sure that all remaining cluster members are up and operational. Use the “clu_get_info –full” command for verification.
  
- 4. Now comes the actual deletion of a cluster member. On another cluster member, run the clu_delete_member command to remove the halted member from the cluster. The clu_delete_member command can be run either interactively or with command line arguments.
  
- 5. Prior to the deletion of the member, if the cluster had an even number of members and a configured quorum disk, then it is important to delete the quorum disk or change the quorum disk’s votes from 1 to 0.

> For more information on adjusting votes for quorum, please see Chapter 17 on Connection Manager.

```
/usr/sbin/clu_quorum -d remove
Collecting quorum data for Member(s): 1 2

Quorum disk successfully removed.
```

Or

```
/usr/sbin/clu_quorum -d adjust 0
Collecting quorum data for Member(s): 1 2

Quorum disk votes successfully adjusted.
```

If, on the other hand, deleting the member reduces the number of members to an even number, then either the quorum disk should be added and/or the quorum disk's votes should be changed from 0 to 1.

```
/usr/sbin/clu_quorum -d add dak5 1
Collecting quorum data for Member(s): 1 2
    Initializing cnx partition on quorum disk : dak5h
Quorum disk votes successfully adjusted.
```

Or

```
/usr/sbin/clu_quorum -d adjust 1
Collecting quorum data for Member(s): 1 2

Quorum disk votes successfully adjusted.
```

## WARNING:

Never add, delete, or modify a quorum disk while either the clu_delete_member or the clu_add_member commands are in process.

## 11.7.3 Execution of the `clu_delete_member` Command

In our example, let’s execute the `clu_delete_member` interactively. Like the other commands needed to create a cluster or to add a new cluster member, the `clu_delete_member` command reveals exactly what it will do and then asks the user if he wants to continue.

```
# /usr/sbin/clu_delete_member

This is the TruCluster Delete Member Program

You will need the following information in order to delete a member from
the cluster:

        -- Member ID (1-63)

The program will prompt for this information, offering a default
value when one is available. To accept the default value, press Return.
If you need help responding to a prompt, either type the word 'help'
or type a question mark (?) at the prompt.

The program does not begin to delete the member until you answer
all the prompts, and confirm that the answers are correct.

Deleting a member involves the following steps:

        Removing the files from the member boot disk. (If accessible)
        Removing member specific areas from the /, /usr, and /var file systems.
        Removing the deleted members entries in shared configuration files.

Do you want to continue deleting a member from this cluster? [yes] : yes
```

Next, the `clu_delete_member` command prompts for the cluster member to be deleted. If this cluster member is not halted and ready to be deleted, do not proceed and please review section 11.7.2.

In our example, we are deleting cluster member3.

```
A member ID is used to identify each member in a cluster.
Each member must have a unique member ID, which is an integer in
the range 1-63, inclusive.

Enter a cluster member ID []: 3
Checking cluster member ID: 3

You entered '3' as the member ID.
Is this correct? [yes]: yes

You entered the following information:

        Member's ID: 3

If any of this information is incorrect, answer 'n' to the following
prompt. You can then enter the correct information.

Do you want to continue to delete a cluster member? [no] yes
```
