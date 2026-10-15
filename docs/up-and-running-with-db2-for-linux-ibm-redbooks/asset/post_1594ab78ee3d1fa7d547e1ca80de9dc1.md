
selected this option). Otherwise you will need to create a new instance using db2icrt after installation.

9. Select how the instance will be used. Check off Partitioned instance (Figure 2-14). This means that the instance will be used in a partitioned database. The machine that you are currently using will host the instance-owning database partition server.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_76_0.png)

Figure 2-14 Select how instance will be used

10. Set user information for the DB2 instance owner. By default, DB2 Setup creates a new user db2inst1 in group db2grp1. You may change user and group names, or configure an existing user to the new DB2 V8 instance by selecting the Existing user option. Note that the default home directory is in /home. You must change the instance home directory to a DB2-specific directory, such as /db2home, that will be NFS-exported to remaining machines participating in the partitioned database.

11. Set user information for the fenced user. This user is responsible for executing fenced user defined functions, such as UDFs and stored procedures. You should also place this home directory in a directory that is shared across the partitioned servers, such as /db2home.

12. Prepare the DB2 tools catalog. You require a DB2 tools catalog if you plan to use the Task Center or scheduler. It is a database that stores task metadata. You may also create a DB2 tools catalog after installation using the CREATE TOOLS CATALOG command, but it's much easier to let DB2 Setup create it for you now.

13. Specify a local database to store the tools catalog. Here you specify which instance, database, and schema in which to store the tools catalog.

14. Set up the administration contact list. The administration contact list stores administrator contact information, and is used for notifying administrators when a database requires attention. You may create a new contact list that is stored locally, or use an existing global contact list that resides on a remote DB2 server. If you check off the Enable notification box, your system will search for an available SMTP server that will be used for e-mail notifications.

> Note: If there is no SMTP server set up, you may set it up after installation by using the DB2 CLP (Command Line Processor). Refer to page 71 for setup instructions.

15. Specify a contact for health monitor notification. By default, a health monitor runs on the DB2 instance you are setting up. The DB2 health monitor will send a notification e-mail to this person at the specified e-mail address when a health indicator threshold is breached. If you check off Address is for a pager, the notification message will be sent to the contact's pager.

> Note: If you choose to Defer task until after installation is complete, you may specify contacts after installation using the Task Center or Control Center. In the Control Center, click the Contacts icon which is located in the taskbar under the Tools menu. Refer to page 71 for setup instructions.

16. Start copying files and create response files. This window provides a summary of your installation and configuration settings. Scroll through this window to verify that your settings are correct, then click Finish.

## Step 2 - Use response file to install DB2 on remaining machines

After performing a partitioned installation, the DB2 Setup wizard creates two response files: db2ese.rsp and db2ese2.rsp. The db2ese.rsp response file contains instructions to create an instance, instance-owning and fenced users, as well as the tools catalog database (if selected during install). The db2ese2.rsp response file only installs the appropriate DB2 filesets, specifies DAS properties, and specifies languages to install. Only use the db2ese2.rsp response file when installing database partition servers on participating computers.

The secondary response file, db2ese2.rsp, looks something like this:

```
**************************************************
* Generated response file used by the DB2 Setup wizard
* generation time: 10/21/02 10:43 AM
**************************************************
* Product Installation
LIC_AGREEMENT = ACCEPT
PROD = ENTERPRISE_SERVER_EDITION
INSTALL_TYPE = TYPICAL
**************************************************
* Das properties
**************************************************
```
