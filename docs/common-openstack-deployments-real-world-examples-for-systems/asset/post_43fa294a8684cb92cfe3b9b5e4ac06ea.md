
# Vendors and Hybrid Clouds

> *Never think you've seen the last of anything.*
>
> Eudora Welry

Much of what has been covered so far has sought to explain how to run OpenStack in a contained environment as something you run yourself, whether you're building an infrastructure for use within your organization or are building a compute cloud for customers. In this chapter we'll explore the ecosystem beyond this by talking about how vendors can help with deployments and how you can also leverage public clouds for what may become a hybrid cloud environment. Finally, we walk through how OpenStack enables you to avoid vendor lock-in with some examples of organizations that have successfully run their infrastructure across multiple clouds.

## Vendor Ecosystem

No tour of OpenStack would be complete without mentioning the vast vendor ecosystem that has built up around OpenStack. There are various companies that have gotten involved with supporting OpenStack, including:

- Traditional customer hosting companies that have recently moved to offering cloud solutions
- Well-established technology companies that have now found their customers wanting a cloud solution
- Completely new companies that have sprung up to specifically offer cloud-centric solutions

These companies will offer a range of services from public to private. We'll cover public services in more depth later in the chapter. Private offerings can range anywhere from coming into your organization and building a full OpenStack deployment to more specific offerings that promise you a solution, like object storage for the sharing of files securely within your organization. As a technologist, understanding the fundamentals of what is going on in your environment is valuable, but these companies come in with the expertise needed to maintain and scale the deployment as your needs change.

If your organization is large enough that you can devote full-time staff to managing your OpenStack-driven environment, there are also vendors who specialize in training and consulting services. These services are valuable for when your team needs to learn more about a specific component of OpenStack or simply is seeking some solid expertise to get over some kind of hurdle you're facing.

The OpenStack Foundation maintains a Marketplace to find vendors at http://www.openstack.org/marketplace/. This marketplace also provides a tour of some of the distributions and appliances that are built around OpenStack and seek to make deployment and management easier. These distribution offerings almost always need vendor interaction for you to explore, but there are some that offer community editions or other simplified samples of their products if you wish to explore them on your own.

In earlier chapters we used Puppet to deploy OpenStack. Some vendors use these open source Puppet modules or others covered in Appendix B, "Other Deployment Mechanisms," but oftentimes they have built their own or added on top of the open source options. It's valuable to ask how they're doing a deployment, so you can become familiar with their tooling so you know how the pieces are coming together.

Beyond just deployment mechanisms, as you explore the vendor ecosystem you should keep in mind that you'll likely be moving into other proprietary software components. The base is still OpenStack, but the tooling around it will likely be something developed or licensed by the vendor to provide value to their customers over their competitors. It's important to understand this as you get into licensing agreements, so you can make the appropriate decisions along with your legal department.

# Public and Hybrid Clouds

Beyond simply running OpenStack on your own, you can become a user of OpenStack clouds by exploring public clouds or leveraging a hybrid cloud environment in your organization.

## Public Clouds

The OpenStack Marketplace mentioned earlier has a section completely devoted to public clouds. As discussed in depth in Chapter 7, "Public Compute Cloud," a public cloud is run by a third party, and you are able to interact with it to spin up instances (typically virtual machines), add block storage to your instances, interact with object storage or manage networking between your instances. It may even be somewhat transparent to you that you're using OpenStack, aside from your familiarity with the user-level tooling, as administration of OpenStack itself is handled by the vendor.

With the capability to simply hook in to a public cloud without handling maintenance and scaling, this is a very compelling option for many organizations. Public clouds can get you the ability to grow exponentially and leverage the services OpenStack provides without a large up-front investment or making it a core competency of your organization. As you evaluate the options, there are several points to keep in mind centered around location, cost and data sovereignty and security.

## Location

One of the most common practical considerations an organization may have is the collection, processing and storage of data. If you're a web-based organization and all of your data is coming from customers who interact with your company over the Internet, it may make a lot of sense to manage this data in the cloud. You can leverage data centers around your country and the world provided by your public cloud vendor without having to build that out yourself, and the data is just as close to you from your customers as something you might serve up from your own data center.

On the other hand, if your organization is doing more in-house data processing, like collecting and passing data between machines that do work on-site or downloading it from a specially tuned device that only has access to a single location, you may need to evaluate whether a public cloud makes sense for you. There are certainly still the scaling and geographically distributed risk-mitigation benefits, but your organization becomes heavily dependent upon a fast and reliable Internet connection. This can be a costly investment and introduce more risk into your environment. A consideration here may be using public clouds as a backup location.

A big driver for other organizations may be established corporate IT policy or PCI Security Standards, so it's important to be aware of the specific requirements within your organization.

## Cost

Running OpenStack in-house can be expensive in terms of the investment in hardware, data center space and staff. However, many organizations find that once they reach a certain scale, this price works out for them better than continuing to pay a vendor for use of their public cloud.

Some of the things to consider when evaluating cost and the benefits you gain from using a public cloud include the following:

- **Growth potential:** Will your infrastructure continue to grow as your organization succeeds?
- **Age, size and maturity of your organization:** Your organization may have leveraged public clouds early on, so an investment didn't need to be made in hardware, space and staff. As the organization continues to mature and succeed, it's vital to do regular re-evaluations to see whether that investment now makes sense.
- **Proprietary offerings that you need:** Does the public cloud you're using offer features you can't find either in open source or through strategic use of in-house development? Early stage vendor lock-in is common, and it's important to regularly evaluate what you depend upon and when or if it ever makes sense to bring this in-house.
- **Core competencies:** Your organization may make a decision that they don't want to be in the business of paying a team of engineers to manage a private infrastructure. Make sure this discussion happens so that use of the public cloud can continue to be justified and budgeted for.

As you can see, there is often a time when companies decide to stop using public clouds, but this is not universally true. In the name of core competencies for a company, many choose to use public clouds long term in order to focus their development efforts elsewhere.

## Data Sovereignty and Security

Sometimes overlooked by companies when they start using public clouds, the topic of data sovereignty is not one that should be ignored. To quickly define it, data sovereignty is the concept in which data processed and stored is subject to the laws of the country in which it is located. On a day-to-day basis, users of the cloud are not familiar with where their photos are stored or where their streaming music comes from, but as the person working to place that data, it’s important to keep your customers safe by being familiar with where that data is stored and the laws that govern that. When evaluating a public cloud platform, be aware of where the data centers are and your options for moving it. This potential risk can be weighed against things like latency when placing data far outside your customer range and cost that comes from hosting in less popular locations for data centers or countries.

It’s also important to be familiar with data security laws in your country. In the United States there are federal laws around the storing of everything from medical data (HIPAA) to financial data (FACTA) to data about children (COPPA). This is in addition to any state and local regulations that may be in place. It’s important to do an evaluation of the type of data you’ll be storing and make sure your public cloud provider is able to meet your data security requirements on the infrastructure side.

## Hybrid Clouds

Beyond the topic of simply leveraging public clouds, many organizations now take advantage of hybrid clouds, which are a mix of both public and private clouds, sometimes even spanning across multiple public clouds.

### Uses

To begin with a series of real world examples like you’ve seen in earlier chapters, the following are a couple places where hybrid clouds are used today.

### OpenStack Infrastructure Team

On a day-to-day basis, the development teams within the OpenStack project submit hundreds of patch proposals that all need tests to be run on them before their peers review the code for inclusion. The OpenStack Infrastructure team handles the thousands of tests kicked off per day from these proposals by running a fleet of OpenStack instances across multiple public clouds, multiple private clouds run by companies to support specific components of the project that need specialized testing and a private “infra-cloud” that the team manages itself to expand onto the donated resources provided by the public cloud companies.

The tooling for interaction with all these clouds is similar as they all use OpenStack. The team has discovered that there are small differences that crop up between how different companies structure their public and private clouds, but these typically can be overcome
