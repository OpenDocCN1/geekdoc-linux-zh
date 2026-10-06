
# UNIX SYSTEM MANAGEMENT PRIMER PLUS

custom ticket categories escalation status ticket status

FIGURE 5.3
Numerous options are available when editing a new ticket in Remedy.

![](img/894492738e879267320b8d6f9a044180_155_0.png)

| ID | Date | Priority | Status | Category | Type | Item | Summary |
|---|---|---|---|---|---|---|---|
| HD00000000744 | 7/15/2001 | High | Open | Ticket | Other | Remedy Test | |
| HD00000000745 | 7/15/2001 | Low | Closed | Ticket | Other | Remedy Test | |
| HD00000000746 | 7/15/2001 | Medium | Closed | Ticket | Other | Remedy Test | |
| HD00000000747 | 11/6/2001 | Low | Closed | Ticket | Other | Testing notification | |

| Category | Business Code | Supported | ClosedCode | Successful | Status | Closed | Unlock |
|---|---|---|---|---|---|---|---|
| Type | | | Enabled? | No | | Pending | |
| Item | | | | Owner-Name | | | |

| General Activity | Request information | Duplication | Solutions | Related Items | Web-Submission |
|---|---|---|---|---|---|---|
| Case ID | | | | Created Acc Mgr | | |
| Priority | | | | Copied Implementation Mg | | Customer Status Summary |
| Urgency | | | | Partner Name | | |
| Case Type | Problem | | | Table Name | | |
| Source | | | | Tekla Ticket Number | | |

custom forms

![](img/894492738e879267320b8d6f9a044180_155_1.png)

# Database Integration with Remedy

Remedy uses Oracle as its back-end for storing trouble ticket data. There are benefits to using a separate relational database for the data store. You can take advantage of advanced querying functionality to put together complex queries listing all tickets assigned to your network engineers that are over two weeks old and still open. In addition, because the base is a completely separate application, you can easily integrate it with other applications like reporting software (such as Crystal Reports) and network monitors.

# Support Tools at a Small Market Research Firm

Three system administrators at a two-year-old online market research firm support ten developers on their Unix infrastructure of 30 servers, and 70 run-of-the-desk PC users. This firm has no formal help desk to speak of, and handling requests by email, phone, and hallway conversations is becoming cumbersome for both the administrators and the regular employees. The IT department does not have much money to spend on non-production items, and there is no need for a large-scale help desk system.

This company eventually chose to use RT (Request Tracker), a freely available source help desk package. RT runs on any Unix platform, requires only Perl and MySQL (also freely available), and is easy to administer. It has both command-line and Web-based front ends, as well as automatic ticket creation through an email gateway. Like Remedy, RT has a database

# Chapter 5 • SUPPORT ADMINISTRATION

back end that can be used to search for historical data, but by the Web-based front end is much less customizable.

RT enables you to put users into groups, create ticket "queues" that the various groups can access (see Figure 5.4), assign tickets to individual users, and assign actions to certain events (that is, you can receive an email when a ticket's log is updated). However, you cannot arbitrarily add new fields to a ticket in RT, as in Remedy; the fields are limited to those supplied by RT, including owner, status, and priority. But remember, because RT is an open source product, it can be changed to meet the needs of the company.

# FIGURE 5.4

RT organizes tickets into queues that can be viewed by different groups of users.

![](img/894492738e879267320b8d6f9a044180_156_0.png)

RT meets the needs of the company. Installation and configuration are so easy that

# Advertising Your Support

The message of the day is a simple text file, located at /etc/motd, that is displayed every time a user logs in.

# SYSTEM MANAGEMENT PRIMER PLUS

The message of the day is a simple text file, located at /etc/motd, that is displayed every time a user logs in.

