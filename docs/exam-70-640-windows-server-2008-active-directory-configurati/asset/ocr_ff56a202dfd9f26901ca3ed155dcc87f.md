+   Table 4-3
+   (continued)


| ROLE | IMPACT OF UNAVAILABILITY | ACTION |
|---|---|---|
| PDC Emulator | Affects network users who are attempting to log on from down-level workstations. | Immediately seize the role to an alternate domain controller if users are affected. |
| | An outage of the PDC Emulator role will be quite visible because clients will be unable to log on to the domain or change their passwords. You will also be unable to raise the domain functional level of a domain. | If the failure is not permanent, the role can be returned to the original domain controller when it comes back online. |
| Infrastructure Master | Temporary outage will not be visible to users or administrators. | If failure is deemed permanent, seize the role to a chosen standby Infrastructure Master that is not a global catalog server in the same site. |
| | Outage will be noticeable if a recent request is made to rename or move a large number of objects, as well as inconsistencies with universal group memberships if the outage lasts an extended period of time. | If the failure is not permanent, the role may be seized and then returned to its original provider when it comes back online. |


# VIEWING THE FSMO ROLE HOLDERS

To view the domain-wide roles of RID Master, PDC Emulator, or Infrastructure Master, complete the following procedure. To view the forest-wide FSMO role holders, complete the second and third procedure in this section.

# VIEW THE RID MASTER, PDC EMULATOR, OR INFRASTRUCTURE MASTER FSMO ROLE HOLDERS

**GET READY.** Before you begin these steps, you must be logged on as a member of the Domain Admins group of the domain that you are querying.

+   1. Open the **Active Directory Users and Computers** MMC snap-in.
+   2. Right-click the **Active Directory Users and Computers** node, click **All Tasks**, and select **Operations Masters**, as shown in Figure 4-5.

+   Figure 4-5
+   Operations Masters dialog box

![](bbox=[0.25, 0.72, 0.55, 0.96])