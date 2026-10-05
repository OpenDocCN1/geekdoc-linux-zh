# Organizing your localization

+   - Users that misbehave in minor ways should be interviewed before being chastised. Users frequently respond to inefficient administrative procedures by attempting to subvert them, so consider the possibility that noncompliance is an indication of architectural problems.

+   - Customer-centered. Talk to users and ask them which tasks they find difficult. Find ways to make these tasks simpler.

+   - Your personal preferences are yours. Let your users have their own. Offer wherever possible.

+   - When administrative decisions affect users' experience of the system, be aware of the reasons for your decisions. Let your reasons be known.

+   - Keep your local documentation up to date and easily accessible. See page 1200 for more information on this topic.

# Organizing your localization

If you size a thousand computers and each computer has its own configuration, you will spend a major portion of your working time figuring out which box has a particular problem and another doesn't. Clearly, the solution is to make every computer the same—right? But real-world constraints and the varying needs of users typically make this impossible.

There's a big difference in administrability between multiple configurations and countless configurations. The trick is to split your task into manageable bits. You will find that some parts of the localization apply to all managed hosts, others apply to only a few, and still others are specific to individual boxes.

In addition to performing installations from scratch, you will also need to roll out updates. Keep in mind that individual hosts have different needs for currency, stability, and uptime.

A prudent administrator should not roll out new releases in masse. Instead, rollouts should be staged according to a gradual plan that accommodates other groups' needs and allows time for problems to be discovered while their potential to cause damage is limited. Never update critical servers until you have confidence in the changes you are contemplating, and Friday until you're prepared for a long weekend in front of the terminal.¹¹

However you design your localization system, make sure that all original data is kept in a revision control system. This precaution lets you keep track of changes which have been thoroughly tested and are ready for deployment. In addition, it lets you identify the originator of any problematic changes. The more people involved in the process, the more important this consideration becomes.

11. Security patches are a possible exception to this rule. Plug security holes as soon as they are. On the other hand, security patches sometimes introduce bugs.

![](bbox=[0.945, 0.645, 0.993, 0.725])