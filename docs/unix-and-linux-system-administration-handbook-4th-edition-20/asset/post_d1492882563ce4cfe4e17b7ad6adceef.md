
## Common functions of ticketing systems

### The foundation: the ticketing and task management system

A ticketing and task management system lies at the heart of every functioning IT group. Having a good system in place will help staff avoid two of the most common workflow pitfalls:

- Tasks failing through the cracks because everyone thinks they are being taken care of by someone else
- Resources wasted through duplication of effort when multiple people work on the same problem without coordination

## Common functions of ticketing systems

A trouble ticket system accepts requests through various interfaces (email, web forms, and command lines being the most common) and tracks them from mission to solution. Managers can assign staff to groups or individual staff members. Staff can query the system to see the queue of pending tickets and perhaps resolve some of them. Users can find out status of a request and see who is working on it. Managers can extract high-level information such as

- The number of open tickets
- The average time to close a ticket
- The productivity of sysadmins
- The percentage of unresolved (rotting) tickets
- Workload distribution by time to solution

The request history stored in the ticket system becomes a history of the problems with your IT infrastructure and the solutions to those problems. If that history is easily searchable, it becomes an invaluable resource for the sysadmin staff.

Resolved trouble messages can be sent to notify sysadmins and trainees, inserted into a FAQ system, or just logged. New staff members can benefit from receiving copies of closed tickets because those tickets include not only technical information but also examples of the tone and communication style that are appropriate for use with customers.

Like others, your ticketing system's historical data can potentially be used against your organization in court. Follow the document retention guidelines set up by your legal department.

Most-requesting systems automatically confirm new requests and assign them a tracking number that submitters can use to follow up or inquire about the request's status. The automated response message should clearly state that it is just a confirmation. It should be followed promptly by a message from a real person explaining the plan for dealing with the problem or request.

## Ticket ownership

### Work can be shared

From a customer's point of view, good assignment system is one that routes problems to a person who is knowledgeable and can solve the problems quickly and completely. From a managerial perspective, assignments need to be challenging to the assignee so that the staff continue to grow and learn in the course of their jobs. Your job is to balance the need to play to employee's strengths with the need to keep employees challenged, all while keeping customers and employees happy.

Larger tasks can be anything up to including full-blown software engineering projects. These tasks may require the use of formal project management and software engineering tools. We do not describe these tools here; nevertheless, they are important and not be overlooked.

Sometimes sysadmins know that a particular task needs to be done, but they don't do it because the task is unpleasant. A sysadmin who points out a neglected, unsigned, or unpopular task is likely to receive that task as assignment. This creates a conflict of interest because it motivates sysadmins to remain silent regarding such situations. Don't let that happen at your site; give your sysadmins an avenue for pointing out problems. You can allow them to open tickets without assigning an owner or assigning themselves to the issue, or you can create an email alias to which issues can be sent.

## User acceptance of ticketing systems

Receiving a prompt response from a real person is a critical determinant of customer satisfaction, even if the personal response contains no more information than the automated response. For most problems, it is far more important for the submitter to know that the ticket has been reviewed by a real person than it is to fix the problem immediately. Understand that administrators receive many requests, and they're willing to wait a fair and reasonable time for your attention. But they're not willing to be ignored.

## Sample ticketing systems

The mechanism through which users submit tickets affects the perception of the system. Make sure you understand your organization's culture and your users' preferences. Do they want a web interface? A custom application? An email alias? Maybe they're only willing to phone calls!

It's also important that administrators take the time to make sure they understand what users are actually requesting. This sounds obvious, but think back to the last five times you emailed a customer service or support allies. We bet there were at least a couple of cases in which the response seemed to have nothing to do with the question—not because those companies were especially incompetent, but because accurately parsing tickets is harder than it looks.

Once you've read enough of a ticket to develop an impression of what the customer is asking, the rest of the ticket starts to look like "blah blah." Fight! Clients waiting for a ticket to find their way to a human, only to learn that the request has been misinterpreted and must be submitted or restarted. Back to square one.

Tickets are often vague or inaccurate because the submitter does not have the technical background needed to describe the problem in the way a sysadmin would. That doesn't stop users from making their own guesses as to what's wrong, however. Sometimes these guesses are perfectly correct. Other times you must first decode the ticket to determine what the user thinks the problem is, then trace back along the user's train of thought to intuit the underlying problem.

## Sample ticketing systems

Tables 32.1 and 32.2 summarize the characteristics of several well-known ticketing systems. Table 32.1 shows open source systems, and Table 32.2 shows commercial systems.

### Table 32.1 Open source trouble ticket systems

| Name | Input* | Lang | Backᵇ | Web site |
|---|---|---|---|---|
| Double Choco Latte | W | PHP | PM | dcl.sourceforge.net |
| Mantis | WE | PHP | M | mantisbt.org |
| OTRS | WE | Perl | PMOD | otr.org |
| RT: Request Tracker | WE | Perl | M | bestpractical.com |
| Scarab | W | Java | M | scarab.tigris.org |
| Trouble Ticket Express | WE* | Perl | FMᵇ | troubleticketexpress.com |

> a. Input types: W = web, E = email
> b. Back end: M = MySQL, P = PostgreSQL, O = Oracle, D = DB, F = flat files
> c. Email and MySQL options require the purchase of an add module (but they're cheap).

We like Mantis a lot. It was originally developed to track bugs in the software for a video game. It runs on Linux, Solaris, Windows, Mac OS, and even OS/2. Mantis

## Chapter 32 Management, Policy, and Politics

Mantis is lightweight, simple, easily modifiable, and customizable. It requires MySQL, PHP, and a web server. But its most important feature is good documentation!

Another nice system is OTRS, the Open Ticket Request System. OTRS features interfaces for both customers and sysadmins, as well as an email interface. OTRS is highly customizable (e.g., greeting messages configurable by queue) and can even log the time spent on a ticket.

Table 32.2 shows some of the commercial alternatives for request management. Since the web sites for commercial offerings are mostly marketing hype, details as the implementation language and back end are not listed.

### Table 32.2 Commercial trouble ticket systems

| Name | Scale | Web site |
|---|---|---|
| EMC Ionix (Infra) | Huge | infra-corp.com/solutions |
| HEAT | Medium | frontrange.com |
| Remedy (now BMC) | Huge | remedy.com |
| ServiceDesk | Huge | ca.com/us/service-desk.aspx |
| Track-It | Medium | numarasoftware.com |

Some of the commercial offerings are so complex that a person or two dedicated to maintaining, configuring, and keeping them running (you know who you are, Remedy and ServiceDesk). These systems are appropriate for a site with a huge IT staff but are a waste for the typical small, overworked IT.

## Ticket dispatching

In a large group, even one with an awesome ticketing system, one problem remains to be solved: it is inefficient for several people to divide their attention between the task they are working on now and the request queue, especially if requests come in email to a personal mailbox. We have experimented with two solutions to this problem.

Our first try was to assign half-day shifts of queue duty to staff members in our sysadmin group. The person on duty would try to answer as many of the incoming queries as possible during a shift. The problem with this approach was that everybody had the skills to answer all questions and fix all problems. Answers were sometimes inappropriate because the person on duty was not really familiar with the customers, their environments, or the specific support contracts they covered. The result was that the more senior people had to keep an eye on things and so were not really able to concentrate on their own work. In the end, the quality of service was worse and nothing was really gained.

After this experience, we created a “dispatcher” role that rotates among a group of senior administrators. The dispatcher is responsible for checking the
