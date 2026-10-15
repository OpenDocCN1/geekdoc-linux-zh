
The mechanism through which users submit tickets affects their perception of the system. Make sure you understand your organization’s culture and your users’ preferences. Do they want a web interface? A custom application? An email alias? Maybe they’re only willing to make phone calls!

It’s also important that administrators take the time to make sure they understand what users are actually requesting. This point sounds obvious, but think back to the last five times you emailed a customer service or tech support alias. We’d bet there were at least a couple of cases in which the response seemed to have nothing to do with the question—not because those companies were especially incompetent, but because accurately parsing trouble tickets is harder than it looks.

Once you’ve read enough of a ticket to develop an impression of what the customer is asking about, the rest of the ticket starts to look like “blah blah blah.” Fight this! Clients hate waiting for a ticket to find its way to a human, only to learn that the request has been misinterpreted and must be resubmitted or restated. Back to square one.

Tickets are often vague or inaccurate because the submitter does not have the technical background needed to describe the problem in the way that a sysadmin would. That doesn’t stop users from making their own guesses as to what’s wrong, however. Sometimes these guesses are perfectly correct. Other times you must first decode the ticket to determine what the user thinks the problem is, then trace back along the user’s train of thought to intuit the underlying problem.

## Sample ticketing systems

Tables 32.1 and 32.2 below summarize the characteristics of several well-known trouble ticketing systems. Table 32.1 shows open source systems, and Table 32.2 shows commercial systems.

### Table 32.1 Open source trouble ticket systems

| Name | Inputᵃ | Lang | Backᵇ | Web site |
|---|---|---|---|---|
| Double Choco Latte | W | PHP | PM | dcl.sourceforge.net |
| Mantis | WE | PHP | M | mantisbt.org |
| OTRS | WE | Perl | PMOD | otrs.org |
| RT: Request Tracker | WE | Perl | M | bestpractical.com |
| Scarab | W | Java | M | scarab.tigris.org |
| Trouble Ticket Express | WEᶜ | Perl | FMᶜ | troubleticketexpress.com |
a. Input types: W = web, E = email
b. Back end: M = MySQL, P = PostgreSQL, O = Oracle, D = DB2, F = flat files
c. Email and MySQL options require the purchase of an add-on module (but they’re cheap).

We like Mantis a lot. It was originally developed to track bugs in the software for a video game. It runs on Linux, Solaris, Windows, Mac OS, and even OS/2. Mantis is lightweight, simple, easily modifiable, and customizable. It requires MySQL, PHP, and a web server. But its most important feature is good documentation!

Another nice system is OTRS, the Open Ticket Request System. OTRS features web interfaces for both customers and sysadmins, as well as an email interface. OTRS is highly customizable (e.g., greeting messages configurable by queue) and can even log the time spent on a ticket.

Table 32.2 shows some of the commercial alternatives for request management. Since the web sites for commercial offerings are mostly marketing hype, details such as the implementation language and back end are not listed.

### Table 32.2 Commercial trouble ticket systems

| Name | Scale | Web site |
|---|---|---|
| EMC Ionix (Infra) | Huge | infra-corp.com/solutions |
| HEAT | Medium | frontrange.com |
| Remedy (now BMC) | Huge | remedy.com |
| ServiceDesk | Huge | ca.com/us/service-desk.aspx |
| Track-It! | Medium | numarasoftware.com |

Some of the commercial offerings are so complex that they need a person or two dedicated to maintaining, configuring, and keeping them running (you know who you are, Remedy and ServiceDesk). These systems are appropriate for a site with a huge IT staff but are a waste for the typical small, overworked IT staff.

## Ticket dispatching

In a large group, even one with an awesome ticketing system, one problem still remains to be solved: it is inefficient for several people to divide their attention between the task they are working on right now and the request queue, especially if requests come in by email to a personal mailbox. We have experimented with two solutions to this problem.

Our first try was to assign half-day shifts of trouble queue duty to staff members in our sysadmin group. The person on duty would try to answer as many of the incoming queries as possible during a shift. The problem with this approach was that not everybody had the skills to answer all questions and fix all problems. Answers were sometimes inappropriate because the person on duty was new and was not really familiar with the customers, their environments, or the specific support contracts they were covered by. The result was that the more senior people had to keep an eye on things and so were not really able to concentrate on their own work. In the end, the quality of service was worse and nothing was really gained.

After this experience, we created a “dispatcher” role that rotates monthly among a group of senior administrators. The dispatcher is responsible for checking the
