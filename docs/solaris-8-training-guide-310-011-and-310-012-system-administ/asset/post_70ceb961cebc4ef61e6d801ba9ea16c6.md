
## Apply Your Knowledge

4. A list of User Management tools appears in the right panel. Click the Administrative Roles tool.

5. Click Action in the toolbar located at the top of the SMC window. From the pull-down menu, click Add Administrative Role. The Add Administrative Role window appears. Fill in the fields with the following information:

Role Name: adminusr
Full Name: Administrative Assistant
Description: Admin assistant for performing general administrative tasks
Role ID number: <accept the default>
Role Shell: Administrator's Bourne

6. The next screen asks you to enter a role password. Enter a password that is 6–15 characters long. Click the Next button to proceed.

7. The next window is where you assign the rights. In the middle pane, select System Administrator and click the Add button. Under the Granted Rights pane, it should display System Administrator. Click the Next button to continue.

8. Select a home directory, and click the Next button.

9. In the next window, titled Assign Users to This Role, enter admin1 in the first field, and click the Add button. Click the Next button to continue.

10. When the summary window appears, click the Finish button. The process of assigning a role to a user is complete.

11. Log out and log back in as admin1. Start up SMC, and test the new user role. You should have general system administration privileges such as adding new users, scheduling jobs, and sharing file systems.

## Review Questions

1. Which three statements about Solaris Management Console are true?
A. It provides a graphical means to manage meta devices.
B. It simplifies administration by bringing the system administration tools together in one location.
C. It allows management of all Solaris Management Console servers in one location.
D. It allows a system administrator to delegate administrative tasks to non-root users without giving out the root password.

2. AdminSuite 3.0 is used to accomplish which of these tasks? Choose all that apply.
A. Manage user accounts
B. Manage shared resources
C. Manage disks
D. Manage processes
E. Schedule processes
F. Manage serial ports
G. Set up AutoClients

## APPLY YOUR KNOWLEDGE

3. SMC is used to accomplish which of the following tasks? Choose all that apply.
- A. Manage user accounts
- B. Manage shared resources
- C. Manage disks
- D. Manage processes
- E. Schedule processes
- F. Manage serial ports
- G. Set up AutoClients

4. What are the three components of SMC?
- A. GUI tools
- B. SMC Client
- C. SMC Server
- D. Toolbox Editor
- E. RBAC

5. Which command is used to start up AdminSuite?
- A. It must be started from the Solaris Management Console.
- B. admapp.
- C. solstice.
- D. adminsuite.
- E. smc.
- F. admsvr.

6. What are the main differences, if any, between SMC and AdminSuite 3.0? Choose all that apply.
- A. Only SMC supports Role-Based Access Control.
- B. Only AdminSuite can manage user accounts.
- C. Only SMC can manage disks.
- D. Only AdminSuite can manage printers.
- E. SMC requires SMC Server to be running; AdminSuite does not require a server daemon.

## Answers to Review Questions

1. B., C., D. SMC simplifies administration by bringing the system administration tools together in one location. It also allows management of all Solaris Management Console servers in one location. Finally, it allows a system administrator to delegate administrative tasks to non-root users without giving out the root password.

2. A., B., F. AdminSuite 3.0 provides an integrated suite of tools for administering your Solaris systems. Wizards and dialog boxes provide assistance and direction for managing user accounts, groups, mailing lists, computers/networks, file system mounts/shares, serial ports, log files, and name service domains.

## APPLY YOUR KNOWLEDGE

3. A., B., C., D., E., F. SMC allows you to manage administrative and network services on your servers from a remote location. Using SMC, the administrator can manage system processes, network resources, user accounts, serial ports, and disk partitions both locally and on remote systems.

4. B., C., D. SMC has three components:
- The SMC Client, called SMC or Console
- The SMC Server
- The SMC Toolbox Editor

5. B. To start up AdminSuite, type the following:

```
/opt/SUNWseam/3_0/bin/admapp.
```

6. A., C. The main differences between SMC and AdminSuite 3.0 are that only SMC supports Role-Based Access Control, and only SMC can manage disks.

## OBJECTIVES

The following test objectives are covered in this chapter:

### Understand Role-Based Access Control
- Traditional superuser-based systems grant full superuser powers to anyone who can become superuser. With Role-Based Access Control (RBAC) in the Solaris 8 operating environment, administrators can assign limited administrative capabilities to non-root users. This chapter describes RBAC with regard to Solaris security.

### Understand RBAC Support Databases
- RBAC relies on four databases to provide users with access to privileged operations. This chapter describes the RBAC databases and configuration commands.

## CHAPTER 20

## Role-Based Access Control (RBAC)

- **Introduction** 731
- **Using RBAC** 731
- **RBAC Components** 737
  - Extended User Attributes (user_attr) Database 738
  - Authorizations (auth_attr) Database 740
  - Rights Profiles (prof_attr) Database 742
  - Execution Attributes (exec_attr) Database 745
- **Summary** 747
- **Apply Your Knowledge** 749

The following strategies help you prepare for the exam:
- Know the terms that I've provided in the Key Terms section located at the end of this chapter. Be prepared to state the purpose of RBAC with regard to Solaris security. Also be prepared to select the statements that describe RBAC database features.
- Practice using RBAC to become familiar with its features. On a Solaris system, go through the step-by-step examples that are provided in this chapter.

## INTRODUCTION

Granting superuser access to non-root users has always been an issue in UNIX systems. In the past, you had to rely on a third-party package, sudo, to provide this functionality. The problem was that sudo was an unsupported piece of freeware that had to be downloaded from the Internet and installed onto your system. In extreme cases, the system administrator had to set the UID permission bit on the file so that a user could execute the command as root.

With Role-Based Access Control (RBAC) in the Solaris 8 operating environment, administrators can assign limited administrative capabilities to non-root users. This is achieved through three new features:
- Authorizations. User rights that grant access to a restricted function.
- Execution profiles. Bundling mechanisms for grouping authorizations and commands with special attributes; for example, user and group IDs or superuser ID.
- Roles. Special types of user accounts intended for performing a set of administrative tasks.

> CAUTION
Most often, you will probably use RBAC to provide superuser access to administrative tasks within the system. Be careful to exercise caution to avoid creating security lapses by providing access to administrative functions by unauthorized users.

## USING RBAC

To better describe RBAC, it's easier to first describe how a system administrator would utilize RBAC to delegate an administrative task to a non-root user in a fictional setting at Acme Corp.

At a fictional company called Acme Corp., the system administrator is overwhelmed with tasks. He is going to delegate some of his responsibility to Neil, a user from the engineering department who helps out sometimes with system administration tasks.

The system administrator first needs to define which tasks he wants Neil to help out with. He has identified three tasks:
- Change user passwords, but not add or remove accounts
- Mount and share file systems
- Shut down the system

In RBAC, when we speak of delegating administrative tasks, it is referred to as a role account. A role account is a special type of user account that is intended for performing a set of administrative tasks. It is like a normal user account in most respects, except that users can gain access to it only through the su command after they have logged into the system with their normal login account. A role account is not accessible for normal logins, for example, through the CDE login window. From a role account, a user can access commands with special attributes, typically the root user IDs, which are not available to users in normal accounts.

At Acme Corp., the system administrator needs to define a role username for the tasks he wants to delegate. Let’s use the role username “adminusr”. After Neil logs in with his normal login name of ncalkins, he then needs to issue the su command and switch to adminusr whenever he wants to perform administrative tasks.

The easiest way to define a role account is by using the Solaris Management Console, as described in the previous chapter. Chapter 19, “Solaris Management Console and Solstice AdminSuite,” provides all of the information you need to define this administrative role for a user. In this chapter, however, I’ll describe how to create a role via the command line.

So far, we have determined that we want to name the role account adminusr. The system administrator creates the role account using the roleadd command. The roleadd command adds a role account to the /etc/passwd, /etc/shadow, and /etc/user_attr files. The syntax for the roleadd command is as follows:

```
roleadd [-c comment] [-d dir] [-e expire] [-f inactive] \
[-g group] [-G group] [-m] [-k skel_dir] [-u uid] \
[-s shell] [-A authorization] <role username>
```

You’ll notice that roleadd looks a great deal like the useradd command described in Chapter 5, “Setting Up User Accounts.” Table 20.1 describes the options for the roleadd command.
