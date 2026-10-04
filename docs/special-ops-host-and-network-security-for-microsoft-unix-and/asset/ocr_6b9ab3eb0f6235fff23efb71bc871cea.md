# Chapter 17 • Architecting the Human Factor

live, and provide suggestions for bridging the gap between internal and external security by working to protect these environments.

Before beginning discussion of how to correct internal security issues in your most sensitive environments, you need to determine where you are most vulnerable. Whereas a financial services company will be most concerned about protecting the privacy and integrity of its clientele's fiscal data, a company whose primary product is software applications will place greater stock in securing their development networks.

Every location your organization hosts sensitive data will have different profiles that you will need to take into account when developing solutions for securing them. In the following sections, I review two groups common to all organizations and address both the threat against them and how to effectively manage that risk.

# Protecting Human Resources and Accounting

Earnings reports. Salary data. Stock options and 401k. Home addresses. Bonuses. This is just some of the information that can be discovered if one gains access to systems used for Human Resources and Accounting. Out of all the internal departments, these two administrative groups provide the richest landscape of potential targets for hostile or mischievous employees. And yet in many organizations, these sit unfiltered on the internal network, sometimes even sporting DNS or NetBIOS names that betray their purpose.

Due to the sensitivity of the information they work with, Accounting and Human Resources departments are usually more receptive to changes in their environment to increase security.The users and managers understand the implications of a compromise of their data, and are quick to accept suggestions and assistance in preventing this type of event. This makes these departments ideal providing grounds for implementing internal security.

Since these groups also tend to work with a great deal of sensitive physical data as well, it is common for these users to be physically segregated from the rest of the organization. Network security in this case can follow the physical example; by implementing similar network-level segregation, you can establish departmental DMZs within the internal network. Done carefully, this migration can go unnoticed by users, and if your first internal DMZ is deployed without significant impact to productivity, you will encounter less resistance when mounting other security initiatives. This is not to imply that you should not involve the users in the deployment; on the contrary, coordination