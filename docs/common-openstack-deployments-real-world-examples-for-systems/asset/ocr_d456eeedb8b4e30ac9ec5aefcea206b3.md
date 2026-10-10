by testing and making changes before they are brought into production. If changes occur to a cloud the team interacts with, they also have a mechanism to specifically disable a single provider without disruption aside from decreased test capacity.

# Government Research Organization

As discussed when talking about public clouds earlier in this chapter, there are many considerations when looking to leverage public clouds in an infrastructure. When you’re a government agency focused on scientific research, many of these are especially important.

One government research organization has been very public about their hybrid cloud deployments and has expanded outside the realm of OpenStack offerings by running a hybrid cloud that uses OpenStack as a private cloud and then reaching out to two entirely different types of public cloud offerings.

In their infrastructure, they’ve leveraged a cloud management platform offered by a vendor that enables them to use similar tools to manage OpenStack and various third-party cloud providers with the same tool set. The management platform vendor handles abstraction of the tools and APIs to make this possible and works closely with their customers to make sure they have access to the various features offered by each public cloud vendor, while still providing a uniform experience across several types of clouds.

This solution has enabled them to store data collected from their scientific instruments locally to their facility for sharing among researchers using their OpenStack private cloud. It has also given them a gateway for citizen scientists and enthusiasts to also interact with subsets of data through web and API-based platforms that run on public clouds.

# Vendor Lock-in

With the sharp rise of open source software in the past decade, many companies have become more aware of the risks involved with proprietary vendor lock-in and how open source software helps them avoid this. Open infrastructure like that provided by OpenStack also plays a role here that is just now being discovered by organizations as they find their licenses and rates for proprietary software cloud solutions and public clouds increasing.

By using OpenStack, you are buying into a solid core of software that you can build the rest of your infrastructure around without worrying about that core rising in cost as you come to depend upon it. Even as you explore the realm of vendor-specific, and even proprietary, OpenStack distributions and appliances, the risk of lock-in is significantly lower because you’re still working with the same core software deep down. You simply have more options when prices increase too much or your vendor becomes unavailable.

Finally, OpenStack runs on commodity hardware. You are not beholden to a hardware vendor who is selling you hardware specific to the software that needs to be purchased at a premium. Existing commodity hardware in a modern virtualized infrastructure should work fine for OpenStack, so you may not need to purchase any new hardware to try OpenStack.