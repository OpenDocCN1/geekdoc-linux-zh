+   - `lprm 157`
+     This removes print job number 157 from the print queue. If the print job is not owned by the user executing lprm and the user is not the system administrator, this fails. Only the user who owns print job 157 and the system administrator can delete this print job.
+   
+   - `lprm all`
+     This removes all the print jobs on the default print queue that were sent by the person invoking lprm. Another similar command for users follows:
+   
+   - `lprm -`
+     When executed as a user, all print jobs sent by that user are deleted from the default printer; when invoked by the system administrator, however, it deletes all the print jobs for the default queue, period.
+   
+   - `lprm all all`
+     This removes all print jobs on all print queues sent by the user who invoked lprm. When executed by the system administrator, this deletes all print jobs on all queues regardless of who sent them.

Combinations of these commands are possible, of course. For instance

```
lprm username all
```

deletes all print jobs sent by the user matching `username` on all print queues.

You can see that the possibilities are extensive when deleting print jobs. Clearly, care must be taken when flipping back and forth as a user and system administrator; because similar syntax performs drastically different tasks with this utility, be sure of who you are logged in as before executing any lprm command. If you are not careful, you might inadvertently delete a job you did not intend to delete.

# ## TAKING CONTROL WITH lpc

The lpq and lprm utilities offer some administration capabilities for users, but certain tasks are absolutely reserved for system administrators. Managing the order of a print queue, the capability to kill and print daemons, the capability to enable or disable a printer queue, and the capability to redirect print jobs are but a few of the things that can be done with lpc, the system administrator’s print control utility.

Among the items just listed, a capability also exists to run lpq and lprm from within lpc. It is the one true control center for all print activities on your system.

When invoked, all that is shown is a command prompt that looks similar to the following:

```
lpc>
```

From there, the question mark (?) key can be pressed to see a screen of help items, descriptions, and syntax for each included.

Commands are entered at the lpc> prompt. For instance, when getting a status listing on all the print queues, the output resembles Listing 31.13.