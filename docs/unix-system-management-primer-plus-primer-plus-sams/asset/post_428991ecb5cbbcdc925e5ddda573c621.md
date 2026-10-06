
# UNIX SYSTEM MANAGEMENT PRIMER PLUS

You should be aware of the commitments and unplanned events that might keep administrators from performing their on-call duties. Vacations, company-wide meetings, and sick days can all interfere with your finely tuned schedules. You can either find another administrator to take the place of the unavailable administrator, or designate a backup on-call person for each week, who will remain available in case he or she is needed.

If you are the only person to handle the on-call duties and you need to take a vacation, take the time to train another person, who preferably is familiar with your systems, to handle the common everyday problems. In these cases you might hire another administrator, perhaps at a junior level, if you have more resources to manage these situations.

# Plan for Multiple Emergencies

A system administrator dealing with an emergency escalated through on-call procedures cannot respond to further on-call escalations without additional help. Make sure to have at least two administrators available at any time so a single emergency does not consume all of your on-call resources.

# Regulation

A system administrator who is on-call not only needs to be available at all times, but he or she must also be capable of providing technical support at all times. If you are in charge of developing on-call procedures, you must devise guidelines that govern the conditions and behavior of all staff during their on-call hours. These on-call guidelines should cover the following:

- **Proximity** The on-call administrator should be within a certain maximum distance to the data center at all times. Thirty minutes is usually a safe travel time, though that may need to be adjusted, depending on how far your employees live.
- **Availability** The on-call administrator should take care not to make commitments that would deter his or her ability to deal with problems in a timely manner. That means if you're scheduled for surgery or other commitments that cannot be altered, make sure to arrange your on-call time so it doesn't conflict with those commitments.
- **Ability to perform** The on-call administrator should be able to perform his or her duties at all times. That means you shouldn't drink too much at that party next Friday night if you are on-call! The last thing a company needs is a tipsy engineer tinkering with the inner workings of $100,000 servers.

# Enforcing On-Call Guidelines

You cannot possibly watch over the lives of every system administrator to make sure they comply with on-call guidelines; that of surveillance is intrusive and impractical. You can encourage administrators to follow the guidelines, however, by making on-call response a performance benchmark in their annual reviews. Reviews tied to bonuses and raises have a unique way of making people perform.

# Communication

Communication between the help desk and on-call staff is far and away the most important factor in any on-call procedure. The help desk needs reliable ways to communicate with on-call staff in case of emergency, and the on-call staff needs reliable ways to respond. The advent of the text pager in the 1990s made this kind of communication a breeze. The help desk can send detailed and informative messages to the on-call person; so can a computer that encounters a critical error. Most modern text pagers enable you to send email responses to pages through the pager itself.

Pagers are great, but they aren't a perfect solution. You can easily move outside the pager's signal, especially if you live in a rural area. To avoid such problems, you will need to incorporate backup communication methods into your on-call procedures. Cell phones and home phones are common communication solutions. The help desk should be given the phone numbers of all on-call staff, for use when communication by pager fails.

![](img/894492738e879267320b8d6f9a044180_144_0.png)

# Use Call Forwarding

Many systems support call-forwarding features that will forward unanswered calls to all other numbers. You could use this to forward an unanswered help desk call to a system administrator's phone, and then to the cell of an administrator.

When on-call staff must speak directly with help desk staff, the on-call person should have a direct line into the help desk to avoid any automated answering service or queues that a customer might encounter. Technical support should have a line dedicated to this purpose, or for the help desk person can provide a name and direct phone number in the page or message for the on-call person.

# Escalation Procedures

When trouble tickets need to be transferred to different levels of support within a multi-tiered support system, that move is accomplished by following a set of escalation procedures. These procedures define under what circumstances a ticket can be assigned to a different group and what communication needs to take place supplement the transfer of "ownership" for the problem. Escalation procedures are critical to the proper functioning of any support department, so it is vital to understand the issues you must consider in their design.

# Put the Help Desk in Control

Your first step in developing escalation procedures is to define the role of the help desk. Let people know that the help desk is the primary point of contact for all trouble tickets and that contacting any other department directly to get a problem fixed is unacceptable. This may seem like an easy policy to establish, but enforcing the policy can be difficult.

# UNIX SYSTEM MANAGEMENT PRIMER PLUS

Two types of people resist complying with the tech support "chain of command." One is the person who says, "Well, I hang out with Jeff every day, so I'll just give him a call and see if we can fix our." Friendliness with the technical staff does not give rubber-stamp approval to noncompliance. Another prone to resisting the policy are those who have been with the company forever and say, "Back in the good old days, when we were 16 people strong, I just called George, and things got fixed. Why should I change now? Those in senior-level positions are most prone to this type of response and may be reluctant to change their ways.

So do you make sure people use the help desk to report problems? One way is to promote the virtues and benefits of the help desk. Emphasize that the help desk can manage their problems for them; they'll take your call or email, make sure it gets to the appropriate group to fix the problem, and report back when the status of the problem changes.

Another method is a bit harsher: have your technical staff refuse to hear any problems over phone or email unless it's from the help desk. This is a very effective method of assuring compliance with your policy, but it can also alienate technical groups from the rest of the company, who may help tech support as a group of "elites." Wearing label may be a small price to pay, by laying down a hand and fast "no contact" rule is the only way to bring in the individuals in your company into compliance with necessary tech support policies.

# Notify Staff of Support Policy Changes

When making a support policy change like the "no contact" rule discussed in this section, send an email or memo out to fellow employees in your organization announcing the change and justifying it. Document the problems that the old system was causing and how the new system will work better by, for example, improving communication efficiency.

# Ticket Assignment

Establishing procedures for assigning tickets to responsible personnel gets the right people on the job quickly and prevents any delays in problem resolution. Ticket assignment is one of the help desk's primary responsibilities; it involves

- Identifying the problems in each ticket
* Categorizing the problems
* Deciding which group or groups to assign each ticket
