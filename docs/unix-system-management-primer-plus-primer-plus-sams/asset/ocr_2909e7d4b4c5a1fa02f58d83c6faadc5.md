# UNIX SYSTEM MANAGEMENT PRIMER PLUS

As a system administrator, you can use the sandbox as you fit; you can test patches, upgrade to new operating systems, and swap hardware in and out of servers. Best of all, you can do all of without affecting users in any way. Because you have time and opportunity to uncover bottlenecks, pitfalls, bugs, and other potential problems that may accompany the new technology, you can resolve or avoid those issues before they become problems for the entire organization. While it is not required, you should try to mimic your production environment as closely as possible; this ensures that your test results will be representative of the results you would see in production.

# Use Identical Operating Systems

If you cannot acquire sandbox hardware that is identical to your production hardware, at least load the servers in your sandbox with the same version of the operating system and patch levels as those on your production servers.

Sandbox hardware can be come by. In many small organizations, including start-ups, management is often more concerned with getting production services online and staying within tight budgets. Testing a server that doesn't serve a very obvious and tangible purpose to management won't likely be a high priority. As system administrator, however, you have some persuasive arguments to make that might help management understand why the sandbox environment is a priority.

A well-researched budget is a good place to start. Sandbox hardware should reflect the hardware you have in your production environment, but it does not need to be production quality. Make sure you price used equipment and look at offerings from alternate vendors, who may offer lower prices on certain hardware than your preferred vendor; when management doesn't have to spend a lot of money to fulfill a request, they are much more likely to view the request in a positive light.

Next, hit them with your production values; without a sandbox environment, you'll have to deploy new operating systems and patches on the company's production systems without testing first. Let management know that you're concerned about lost time and revenues if something goes wrong in a new deployment. You have no way of predicting every potential problem without testing. If you can present realistic scenarios of such problems and the potential repercussions of their occurrence, management can assess the business benefits of approving the sandbox environment.

In the best-case scenario, you'll get your servers. In the worst case, you'll have documented evidence of your warnings to management when something does wrong. Subsequent sections in this chapter assume that you have a sandbox environment.