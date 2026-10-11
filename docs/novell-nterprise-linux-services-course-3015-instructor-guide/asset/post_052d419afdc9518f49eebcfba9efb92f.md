
## Part IV: Upload a File for the Team

Do the following:

1. Select the **Logout** link.
2. Using KWrite, create a text file in /home/student called **agenda.txt**.
3. Log in to Virtual Office as **srife** (team owner).
   You must be logged in as the team owner to upload files for the team.
4. On the left, select **Efficiency Project.**
5. On the right under **Files**, select **Upload.**
6. Select **Browse.**
7. Browse to and select /home/student/agenda.txt; then select **Open.**
8. At the bottom of the window select **Notify All Members**; then select **Upload.**
9. Select **Close.**
   The screen refreshes with agenda.txt displayed as an available file.
10. Select the **Logout** link.
11. Log in as **cgrayson.**
12. On the left, select **Efficiency Project.**
    Notice that agenda.txt is available for Chris Grayson to download.

## Part V: Create a Reminder Message for the Team Meeting

Do the following:

1. Select the **Logout** link.
2. Log in as **srife** (team owner).
3. On the left, select **Efficiency Project**.
4. On the right under **Discussion**, select **New Message**.
5. In the Subject field, enter **Team Meeting Reminder**.
6. In the message field, enter **Don't forget the team meeting tomorrow**.
7. Mark **Notify All Members**; then select **Post**.
8. Select the **Logout** link.
9. Log in as **cgrayson**.
10. On the left, select the **Efficiency Project** in the left frame.
11. On the right under Discussion, select the **Team Meeting Reminder** message.
12. Try using other features of Virtual Office.
13. When you finish, close the web browser.

(End of Exercise)

## Summary

| Objective | Summary |
| :--- | :--- |
| 1. Describe Virtual Office | Virtual Office is a web access portal that allows remote users to collaborate and share information with a workgroup team. <br><br> Virtual Office optimizes the concept of self-service for users by letting them set up and manage many of their own networking, information-sharing, and data backup processes. <br><br> Virtual Office also lets users create their own functional teams, called Virtual Teams, for interactive real-time collaboration. <br><br> People who join a virtual team can access shared documents, discussion threads, bookmarks, and a team calendar. All members of the team have access to the team information and services. |
| **1. Describe Virtual Office (continued)** | - With Virtual Office, users can<br>- Locate and set up printers<br>- Set up and maintain passwords<br>- Back up information<br>- Communicate in real time with other users and groups<br>- Publish a personal Web page to provide information to other users<br>- Access important information from any location using any web-enabled device<br>- Bookmark Web pages |
| 2. Install Virtual Office | You can install Virtual Office as an optional component when you install Novell Nterprise Linux Services (NNLS). When you select Virtual Office, the NNLS installation script installs all the components needed on your server. <br><br> Because the Virtual Office main page provides web access to other products installed with NNLS, you need to select the following products during installation if you want to access them from Virtual Office:<br>- eGuide<br>- iFolder<br>- iPrint<br>- NetMail<br><br> The Virtual Office main page displays only shortcut buttons for the products you select. |
| 3. Configure Virtual Office | In iManager, you can configure the following services:<br>- Company Info Service<br>- NetStorage<br>- iPrint<br>- eGuide<br>- ZENworks<br>- Bookmarks<br>- Groupwise Configuration<br>- Lotus Notes Configuration<br>- Microsoft Exchange Configuration<br>- NetMail Configuration<br>- IMAP/POP3 Server Configuration<br>- Public Web Page<br>- Change Password<br><br> You can configure many of the Virtual Office services using the Virtual Office home page. To open the virtual office home page, open a browser window and enter http://server_IP_or_DNS/vo.<br><br> You configure the following services from this location:<br>- Bookmarks<br>- Change Password<br>- Public Web Pages<br>- Virtual Teams<br>- Virtual Team Services |

## SECTION 10 Prepare for the Novell CLE Practicum

Emphasize that these scenarios help students prepare for the NNLS services portion of the practicum.

The scenarios do not include Linux administrator tasks that might be included as part of testing LPI Level 1 certification objectives.

Before students start Scenario 1, you will need to provide them with a clean installation of SuSE\* SLES 8.

In this section, you work through the following scenarios to help you prepare for the CLE practicum:

- Scenario 1: Install NNLS (Required)
- Scenario 2: Business Requirements Document 1
- Scenario 3: Business Requirements Document 2
- Scenario 4: Business Requirements Document 3

The initial scenario is required. You can then select one or both of the remaining scenarios (as time permits) to configure NNLS products.

Scenarios 2, 3, and 4 give you a list of business requirements you need to fulfill as network administrator for your Digital Airlines office.

While some requirements are the same for all 3 scenarios, other requirements can change the nature of how you might test or configure the NNLS services to meet the same requirements.

![](img/d63035f3fce0eaaf97203dde900affb7_284_0.png)

> In a classroom environment, your instructor will provide a clean installation of SuSE\* SLES 8 before you start Scenario 1.

### Scenario 1: Install NNLS (Required)

Digital Airlines is currently using eDirectory™ and other Nterprise™ services on NetWare® to deliver networking services to customers and employees.

However, with the availability of NNLS, the CTO has decided to begin migrating several Nterprise services (such as iFolder® and iPrint) to Linux servers.

You have recently received a document that outlines the business requirements for delivering Nterprise services on Linux in your office, along with a timeline for migration of these services.

To meet these requirements and timeline, you need to begin creating and testing immediately an NNLS configuration in a lab environment that meets the business requirements.

You decide to start with a single Linux server that has NNLS installed.

Do the following:

- Install Mozilla 1.5 and prepare your server for NNLS installation using the parameters assigned to you in class (your *container*, **10.0.0.x**, **DAx**).
  Follow the same instructions you followed in Sections 1 and 2.
- Install all components of NNLS using the defaults assigned to you in class (*your* **container**, **10.0.0.x**, **DAx**).
  Follow the same instructions you followed in Section 2.
- Import the same LDIF file into your tree that you imported in Section 3.
- Run a Health Check of your eDirectory tree to make sure that there are no problems.

### Scenario 2: Business Requirements Document 1

After installing NNLS 1.0 and importing the LDIF file, you implement and test the following business requirements in your lab environment:

- You must be able to subscribe to the 3015 channel and install any updates to NNLS. All man pages for all NNLS services must be accessible from a shell prompt in a terminal session window. You must be able to import and export CSV files to and from eDirectory and back up any CSV files in the output directory.

![](img/d63035f3fce0eaaf97203dde900affb7_286_0.png)

> Use the same basic configuration for your Delimited Text driver that you used in Section 5.

To meet this requirement:

- All employees in the sample.csv file on your hard drive must be imported into a **tempwork.your container** container in your eDirectory tree. All members of the WPU5ERS group in *your container* must be exported to a **pilots.csv** file on your hard drive. To back up CSV files in the output directory, create a script called **backupcsv** that creates a tarball of all CSV files currently in the output directory and it to a /tmp/csvbackup directory. Make sure the /tmp/csvbackup directory has the same permissions as the /tmp directory. Create a cron job that executes the backupcsv script once a week on Friday at 5:00pm.
