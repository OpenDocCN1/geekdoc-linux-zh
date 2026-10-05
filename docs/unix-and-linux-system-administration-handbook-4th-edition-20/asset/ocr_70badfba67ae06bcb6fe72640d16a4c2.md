# Quality control

Later, you may have to collect data showing incompetence, give formal warnings,
set performance goals, and so on.

# Mechanics of personnel management

There is more to integrating a new employee into your infrastructure than just
writing an offer letter. You must be aware of and honor your organization's rules
regarding advertising for positions, trial periods, reviews, and so on.

Another set of chores defines the mechanics of getting a new person settled with
desk, computer, keys, accounts, and sudo access. Your processes should ensure
tat a system administrator helped administer a particular set of servers is not
given carte blanche to administer any system in the company.

Just as important are the policies and procedures to follow when sysadmin
leaves the organization. You need a checklist so you don't forget anything.
Your checklist should include things asch

+   * Removing the user's domain account (LDAP or Access Directory)
* Removing the user's UNIX and Linux accounts
* Removing the user's all from the site's sudoers files
* Collecting keys and access cards (document all keys and cards collected)
* Collecting a company cell phone

Some organizations can print a definitive list of access rights and hardware that
have been given to each employee. This is a great way to make sure you haven't
forgot anything.

In the United States, it's common for employees to give two weeks' notice before
quitting. Some sites forget the two-week period and walk the employee to the
door, immediately revoking all physical and network access. Smart!

# Quality control

Managers set the tone for quality control. Each task should have clear criteria for
completion. In addition to the work inherent in each task, completion criteria
might include

+   * Testing the solution
* Updating local documentation
* Propagating the solution to all affected machines
* Completing the trouble ticket with details of the actions taken
* Getting the test initiator to sign off on the resolution as satisfactory

Even a simple task, such as creating a cron job to help with a daily administrative
chore, should include a testing phase to ensure that the change works as intended.
More complex tasks should include a documented test plan.

Ideally, your IT group would have a culture in which sysadmins take it upon
thems to ensure that each job is done well and completely. But to achieve that