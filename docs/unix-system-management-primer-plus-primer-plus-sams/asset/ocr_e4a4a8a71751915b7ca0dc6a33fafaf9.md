# UNIX SYSTEM MANAGEMENT PRIMER PLUS

Remember, you aren't creating a "to do" list; you're creating a full recipe for recovering each critical service or function.

Using the mail server migration as an example, you can create a list of tasks for moving its ser-vices the primary data center to a disaster recovery center. Here's an example of such a list:

+   1. George: Call Jeff (555-4575), Steve (555-4529), Chad (555-4596), and Mike (555-4526) to begin migration procedure. Call secondary site at 555-1234 to alert them of our dis-ter (5 minutes).
2. Steve: Call tape storage facility at 555-6789 and have them ship most recent tapes to secondary site (5 minutes).
3. Jeff & Steve: Drive to hot site at 1313 2nd Avenue (30 minutes).
4. Steve: Wait for backup tapes to arrive (0 to 2 hours; depends on step 3).
5. Jeff: Verify correct software is installed and configured on DR server (10 min-utes).
6. Steve: Restore mailboxes from backup tapes (1 hour; depends on steps 4 and 5).
7. Jeff: Start mail services on DR server (5 minutes; depends on step 6).
8. Chad: Change DNS to reflect new mail server's address: 10.1.2.3 (5 minutes; depends on step 7).
9. Mike: Test mail services from office. Send a message to the "testing" account and to retrieve the mail. Check headers to verify mail routing through the new server (15 min-utes; depends on step 8).
10. Steve: Schedule regular backups of new server (15 minutes; depends on step 6).

This was a fairly simple, ten-step recipe for migrating mail services from one location to another. Each step notes the person responsible for that step, the exact task (including details such as phone numbers and addresses), the time of the task is expected to take, and any dependencies.

# Use the List as a Guide

In your critical task list, some steps might be able to be performed simultaneously or out of order, depending on the nature of each step. In the critical task list in this chapter, for example, step 10 can easily be performed immediately after step 6, Steve may not want to reschedule backups until the emergency team has verified that everything is functional.

This procedure is just one set of tasks that would need to be performed in a complete mig-ration of services during a disaster. You need a detailed procedural plan for each service that must be recovered following a disaster. You must merge all of these into central plan of attack.

![](bbox=[0.138, 0.715, 0.198, 0.755])