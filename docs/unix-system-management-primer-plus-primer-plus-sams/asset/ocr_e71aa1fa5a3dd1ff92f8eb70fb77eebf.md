Response time failures and other timeouts usually qualify as downtime when measuring service levels and should be recorded as such. If you are lucky enough to be involved in a service level contract negotiation, look for this clause and verify that you can perform at the levels that are specified. If the contract expects a Web site to respond within 5 seconds for every request, make sure your systems can meet that requirement! Both Chapter 6 and Chapter 11 present information that can help you determine whether services can perform as requested, and if not, whether they can be tuned to do so.

# # Observing Production Values

This isn't a book on morality, but every system administrator should know and obey his or her set of production values. *Production values* are the rules that minimize risk on production servers and can prevent outages from occurring in the first place. Production values may differ from organization to organization, and even from person to person, but they should all include your department's commitment to honor these basic promises:

+   * To use production servers appropriately
* To announce all maintenance
* To watch logs and monitors
* To respond quickly to outages

Establishing and honoring production values is essential to establish credibility and respect for you and your IT. To better understand the issues involved in each of the basic values listed here, read the sections that follow.

# # Using Production Servers Appropriately

Systems are often broken down into three categories: development, staging, and production. Each of these system types has a specific use, and the production system is the most critical to the business of your organization. Your first production value should include a commitment to use the production servers as they should be used, to protect your service to your organization.

To use production servers wisely, you need to understand how all three system categories are used. Development systems are used for testing and developing new services. It doesn't matter if development systems are up or down; a business's financial well-being doesn't depend on those systems (although some developers might complain).

Staging systems are where new services are migrated for testing in a production environment before actual deployment onto production systems. Staging systems usually are designed to look exactly like the production environment, so people can get a good idea of how services will behave in production. Not everyone has or can afford a separate staging environment; in case, development systems often play this role.