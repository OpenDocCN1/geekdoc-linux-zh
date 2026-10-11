# Figure 1.2 Placing bastion hosts on an intermediate DMZ segment between a firewall and an Internet access router

![](bbox=[0.13, 0.18, 0.88, 0.41])

# Extranet

The term *extranet* refers to a network segment dedicated to provide services to a set of users who are known to your organization, but are not trusted at the same level as your internal users. For example, you may be asked to offer extranet services to business partners so that you can share proposals and system specification documents. Or perhaps your company is a subcontractor in a multi-vendor integration effort, and needs to make many large files available to other development partners.

Access to extranet servers often requires some form of authentication, although the appropriate access control measures should be in place to ensure that extranet users do not gain access to internal network services. Note that it is perfectly acceptable to place extranet servers in the same DMZ segment as the more public bastion hosts. By doing this you allow outside people access to the material they need to see, but they do not gain access to the internal information of the company that needs to be kept confidential. Figure 1.3 shows the placement of extranet hosts on a DMZ.